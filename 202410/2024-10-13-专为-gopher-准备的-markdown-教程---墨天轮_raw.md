Title: 专为 Gopher 准备的 Markdown 教程

URL Source: https://www.modb.pro/db/87166

Markdown Content:
Markdown 大家应该不陌生，几乎是程序员必须掌握的，甚至很多非程序员也熟知。现在大部分的社区都会支持 Markdown 格式。Markdown 语法相对简单，网上随处可以找到相关教程。因此本文不是一篇 Markdown 语法教程，而是希望通过一个 Go 语言 Markdown 解析库的学习来更深入地了解、掌握 Markdown。

如果你对 Markdown 语法了解很少，这里有一份极简的教程：https://studygolang.com/markdown。

CommonMark 和 GFM
----------------

我们经常会在一些 Markdown 解析库的描述中看到类似这样的话：兼容 CommonMark，支持 GFM 扩展等。

### CommonMark 是什么

这是 Markdown 标准或规范。CommonMark 官网（https://commonmark.org ）提到：

> 由于没有明确的规范，Markdown 解析渲染会有很大差异。因此用户经常会发现在一个系统（例如 GitHub）上渲染正常的文档在另一个系统上渲染不正常。更糟糕的是由于 Markdown 中不存在“语法错误”，所以无法立即发现这类问题。

在 Markdown 处理上“模糊的正确”是不可取的。所以 CommonMark 规范的目的就是消除二义性，制定统一明确的 Markdown 解析渲染规则。

该规范的主要参与者包括：

*   David Greenspan, 来自 Meteor
    
*   Vicent Marti, 来自 GitHub
    
*   Neil Williams, 来自 Reddit
    
*   Benjamin Dumke-von der Ehe, 来自 Stack Exchange
    
*   Jeff Atwood, 前 Stack Exchange 联合创始人，Discourse 创始人
    

从作者阵容我们可以看出，该规范算是众望所归了，因为这几大社区都需要一个标准化的 Markdown。

至于规范的具体内容，有兴趣的可以看官网上的规范定义文档，其中的一些点，在后文介绍 Go 语言的 Markdown 解析器时会介绍。

### GFM 又是什么

有了 CommonMark（标准 Markdown），为什么又会有 GFM？

GFM 是 GitHub Flavored Markdown 的缩写，即 GitHub 风格的 Markdown，它和标准 Markdown 存在一些差异，主要是增加一些功能，所以一般叫做 GFM 扩展。类似的、基于标准 Markdown 的衍生分支有很多，但因为 GitHub 的流行，GFM 几乎成为了最强大的一个，而且各种解析器、编辑器都会支持 GFM。

对于大部分人来说，关于 CommonMark 和 GFM，知道这么多就够了。GFM 规范见：https://github.github.com/gfm/。

Go 语言 Markdown 解析器
------------------

在 GitHub 上一搜，发现 Go 语言 Markdown 解析器不止一个，如何选择呢？一般来说根据 Star 数来。另外，如果是实现某个规范的库，看这个规范有无推荐。比如我们找的是 Markdown 库，看看 CommonMark 有无推荐。

在 List of CommonMark Implementations 列出了各个语言的 CommonMark 实现，其中 Go 语言列出了 4 个。虽然 russross/blackfriday 是最早也是 Star 数最多的 Go 语言 Markdown 解析库，然而它不兼容 CommonMark。

因为 Hugo 从 0.60.0 开始，Markdown 解析器默认使用 yuin/goldmark，之前使用的是 blackfriday。因此本文我们主要通过学习 goldmark 这个解析器来深入学习 Markdown。

### 简介

goldmark 是一个用 Go 编写的 Markdown 解析器。易于扩展，符合标准，结构良好。它兼容最新的 CommonMark 0.29 规范。

该库希望满足如下需求：

*   易于扩展
    

*   与其他轻量级标记语言（例如 reStructuredText）相比，Markdown 在文档表达式方面的表现较差。
    
*   我们可以对 Markdown 语法进行了扩展，例如 PHP Markdown Extra，GitHub 风格 Markdown（GFM）。
    

*   符合标准
    

*   CommonMark 复杂且难以完全实现。
    
*   Markdown 有许多方言。
    
*   GitHub Flavored Markdown 被广泛使用并且基于 CommonMark，有效地提出了 CommonMark 是否是理想规范的问题。
    

*   结构良好
    

*   基于 AST；保留节点的源位置。
    

*   纯 Go 语言实现
    

基于此，该库具有如下一些特性：

*   **符合标准**。goldmark 完全符合最新的 CommonMark 规范。
    
*   **可扩展**。你是否要在 Markdown 中添加 @username 提到谁的语法？你可以轻松地在 goldmark 中实现。你可以添加 AST 节点，用于块级元素的解析器，用于内联级元素的解析器，用于段落的转换器，用于整个 AST 结构的转换器以及渲染器等。
    
*   **性能**。goldmark 的性能与用 C 语言编写的 CommonMark 参考实现 cmark 的性能相当。
    
*   **健壮性**。goldmark 已通过模糊测试工具 go-fuzz 进行了测试。
    
*   **内置扩展**。goldmark 附带了常见的扩展，例如表格，删除线，任务列表和定义列表。
    
*   **只依赖标准库**。
    

### 使用

本文使用的 Go 版本是 1.14.x，依赖管理使用 Go Module。

首先安装 goldmark：

```
$ go get github.com/yuin/goldmark
```

为了方便演示，我们使用 https://studygolang.com/markdown 上的教程作为原始 markdown 内容（部分内容是 studygolang 特有的）。

#### Demo1

代码如下：

```
func demo1() { source, err := ioutil.ReadFile("guide.md") if err != nil {  panic(err) } f, err := os.Create("guide1.html") if err != nil {  panic(err) } err = goldmark.Convert(source, f) if err != nil {  panic(err) }}
```

*   guide.md 存放 https://studygolang.com/markdown 上的原始 markdown 内容，略有增减；
    
*   通过 goldmark 的 Convert 函数将  markdown 转为 html，没有使用任何选项；
    

在项目目录生成 guide1.html，在浏览器中打开，发现存在以下问题：

1.  不支持自动链接，例如 `https://studygolang.com`  
    不会被识别为链接；
    
2.  不支持删除线，即 `~~`  
    ；
    
3.  不支持表格；
    
4.  不支持任务列表；
    
5.  不支持语法高亮；
    
6.  不支持 @；
    
7.  不支持表情；
    

#### Demo2

demo1 中问题 1-4 是 GFM 支持的语法，因此我们可以通过 goldmark 内置的 GFM 扩展实现。

```
func demo2() { source, err := ioutil.ReadFile("guide.md") if err != nil {  panic(err) } f, err := os.Create("guide2.html") if err != nil {  panic(err) } // 自定义解析器 markdown := goldmark.New(  // 支持 GFM  goldmark.WithExtensions(extension.GFM), ) err = markdown.Convert(source, f) if err != nil {  panic(err) }}
```

*   验证上面问题 1-4 发现都解决了；
    
*   这里关于自动链接，有一个小问题：中文标点符号问题。`自动链接：https://studygolang.com`  
    这里的冒号是中文的，因此识别不出来。所以，如果使用自动链接，注意链接前后加上英文空格；或单独链接总是使用 `<>`  
    包裹，这是 CommonMark 支持的语法；
    

#### Dome3

语法高亮问题，虽然 goldmark 库没有内置该扩展，但该库作者在另外一个包实现了，这就是 goldmark-highlighting。

```
func demo3() { source, err := ioutil.ReadFile("guide.md") if err != nil {  panic(err) } f, err := os.Create("guide3.html") if err != nil {  panic(err) } // 自定义解析器 markdown := goldmark.New(  // 支持 GFM  goldmark.WithExtensions(extension.GFM),  // 语法高亮  goldmark.WithExtensions(   highlighting.NewHighlighting(    highlighting.WithStyle("monokai"),    highlighting.WithFormatOptions(     html.WithLineNumbers(true),    ),   ),  ), ) err = markdown.Convert(source, f) if err != nil {  panic(err) }}
```

这是语法高亮后的效果：

![Image 1](https://oss-emcsprod-public.modb.pro/wechatSpider/modb_20210726_8d8d1dac-edef-11eb-bf70-00163e068ecd.png)

*   语法高亮使用的是一个 Go 第三方库：alecthomas/chroma
    

### 学习 goldmark 的设计

上节遗留的问题先不处理，因为涉及到扩展 goldmark，我们先学习下 goldmark 的设计。

该库的主包（github.com/yuin/goldmark）公开的内容不多，一共 3 个类型和 3 个函数。

![Image 2](https://oss-emcsprod-public.modb.pro/wechatSpider/modb_20210726_8de23a12-edef-11eb-bf70-00163e068ecd.png)

#### Markdown 是一个接口

```
type Markdown interface { // Convert interprets a UTF-8 bytes source in Markdown and write rendered // contents to a writer w. Convert(source []byte, writer io.Writer, opts ...parser.ParseOption) error // Parser returns a Parser that will be used for conversion. Parser() parser.Parser // SetParser sets a Parser to this object. SetParser(parser.Parser) // Parser returns a Renderer that will be used for conversion. Renderer() renderer.Renderer // SetRenderer sets a Renderer to this object. SetRenderer(renderer.Renderer)}
```

*   解析器：Parser
    
*   渲染器：Renderer
    
*   解析 markdown 文本并将渲染的结果写入 io.Writer 中
    

从这个接口的定义可以看到，我们可以定义自己的 Parser 或 Renderer 来改变 goldmark 的工作方式。一般我们不需要这么做，只需要使用默认的实现即可，这也就是 DefaultParser() 和 DefaultRenderer() 两个函数的作用。另外，在转换时（Convert）支持指定解析选项。

然而在该包中，我们并没有看到 Markdown 接口的实现类型。很显然，实现类型没有导出。这体现了“依赖抽象而不依赖具体”的设计原则。

看看获取 Markdown 接口实例的 New 函数：

```
func New(options ...Option) Markdown
```

该函数接收一个不定参数：Option，用于控制 Markdown 的行为。这里引出了 Go 中常见的一个设计模式。

Go 不是完全的面向对象语言。当类型中有较多成员，且可以通过外部控制时，根据封装的原则，一般不建议将这些字段导出（公开），但这样一来构造函数就需要能接收很多参数；亦或是希望通过其他方式扩展。在 Go 中有两种较常见的设计方法。

**1）通过另外一个结构体来控制**

这里以 BigCache 这个包为例，该包中的 Config 结构体就是这种设计。这么做有什么好处？

```
func NewBigCache(config Config) (*BigCache, error)
```

一方面控制了 BigCache 类型的行为，避免实例化后可以随意更改，起到了封装的作用。另一方面，让构造函数更简洁，只需要接收一个 Config 即可（注意最好使用 Config 值类型，而不是指针）。而且可以通过提供一些 Config 的默认值来做到更易用，比如 bigcache.DefaultConfig() 函数就是这样的例子。

**2）通过一个函数类型来控制**

前面提到，goldmark 只导出了 Markdown 接口，并没有导出该接口的具体实现类型。那想要控制具体实现类型的行为怎么办呢？这就是 Option 这个函数类型的作用：接收一个 markdown 类型指针（注意这里不是 Markdown 接口，而是实现了该接口的具体类型）

```
type Option func(*markdown)
```

然后构造函数中接收一个 Option 类型的不定参数，来控制 Markdown 的行为。

```
func New(options ...Option) Markdown
```

为了方便使用 ，一般包会提供若干获得 Option 实例的方法。goldmark 包提供了 5 个返回 Option 的函数：

```
// 增加扩展func WithExtensions(ext ...Extender) Option// 允许你覆盖默认的 Parserfunc WithParser(p parser.Parser) Option// 为 Parser 修改配置选项func WithParserOptions(opts ...parser.Option) Option// 允许你覆盖默认的 Renderfunc WithRenderer(r renderer.Renderer) Option// 为 Renderer 修改配置选项func WithRendererOptions(opts ...renderer.Option) Option
```

在 Demo3 中使用了 WithExtensions() 为解析器增加扩展，该函数接收一个 Extender 类型的不定参数。

#### Extender 也是一个接口

该接口用于扩展 Markdown，因此方法接收一个 Markdown 参数：

```
type Extender interface { // Extend extends the Markdown. Extend(Markdown)}
```

由此可见，所谓的 goldmark 扩展，就是一个实现了 Extender 接口的类型。

#### Convert 函数

这是一个为了方便使用的函数，在 Go 语言标准库中有大量这样的设计。

> 针对包的主要类型提供一个默认实例，包级便利函数直接调用该默认实例的相应方法

比如 log 包中的 std 是一个默认的 Logger 实例、net/http 包中的 DefaultClient 是一个默认的 Client 实例。

而 Convert 函数的实现如下：

```
func Convert(source []byte, w io.Writer, opts ...parser.ParseOption) error { return defaultMarkdown.Convert(source, w, opts...)}
```

其中 defaultMarkdown 就是一个 Markdown 的实例：

```
var defaultMarkdown = New()
```

因此最终调用的还是 Markdown 接口的 Convert 方法。

#### New 函数

最后看看该包 New 函数实现：

```
// New returns a new Markdown with given options.func New(options ...Option) Markdown { md := &markdown{  parser:     DefaultParser(),  renderer:   DefaultRenderer(),  extensions: []Extender{}, } for _, opt := range options {  opt(md) } for _, e := range md.extensions {  e.Extend(md) } return md}
```

*   markdown 实现了 Markdown 接口；
    
*   parser 和 renderer 使用 goldmark 包默认的；
    
*   遍历执行 Options；如果 Option 是 Extender，则 md.extensions 会赋上值：
    
    ```
    func WithExtensions(ext ...Extender) Option { return func(m *markdown) {  m.extensions = append(m.extensions, ext...) }}
    ```
    
*   最后遍历执行 Extender 的 Extend 方法；
    

### 小结

从 goldmark 的设计和源码看出，它大量使用接口，包括 Parser 和 Renderer 都是接口，这使得它具有极强的可扩展性。接下来我们会尝试自己实现一个 goldmark 扩展。

自己实现一个 goldmark 扩展
------------------

上面我们遗留了两个问题没有处理，即支持 @ 和 `:+1:`  
这种形式的表情。现在我们通过实现自己的扩展来解决这两个问题。

### 如何实现一个扩展

goldmark 的文档有一些扩展开发的内容，提供了一个 goldmark 处理 markdown 的概要图：

```
            <Markdown in []byte, parser.Context>                           |                           V            +-------- parser.Parser ---------------------------            | 1. Parse block elements into AST            |   1. If a parsed block is a paragraph, apply             |      ast.ParagraphTransformer            | 2. Traverse AST and parse blocks.            |   1. Process delimiters(emphasis) at the end of            |      block parsing            | 3. Apply parser.ASTTransformers to AST                           |                           V                      <ast.Node>                           |                           V            +------- renderer.Renderer ------------------------            | 1. Traverse AST and apply renderer.NodeRenderer            |    corespond to the node type                           |                           V                        <Output>
```

你可能看着有点晕。整体上扩展开发有 4 个工作：

1.  定义一个 AST（抽象语法树）节点（结构体），该节点需要嵌入一个 `ast.BaseBlock`  
    或 `ast.BaseInline`  
    ；
    
2.  定义一个解析器（Parser），实现 `parser.BlockParser`  
    或 `parser.InlineParser`  
    ；
    
3.  定义一个渲染器（Renderer），实现 `renderer.NodeRenderer`  
    ；
    
4.  定义一个 goldmark 扩展，实现 `goldmark.Extender`  
    ；
    

其中 Block 和 Inline 是什么意思？学习过 Web 前端的应该了解。Markdown 和 HTML 类似，将内容元素分为块级元素（Block）和行级元素（Inline）：（块级元素优先级高于行级元素）

*   块级元素：块引用（\>）、列表项和列表（列表只能包含列表项）、分隔线、标题、代码块、某些 HTML 块、段落等
    
*   行级元素：内联代码（`code`  
    ）、强调、加粗、链接、图片、某些 HTML 标签、文本等
    

根据以上的内容，要自己实现一个扩展还是有难度的。好在 goldmark 中内置了一些扩展，可以作为参考。

### GFM 的 strikethrough 扩展源码学习

CommonMark 是不支持删除线（strikethrough）的，而 GFM 支持。因此 goldmark 通过 strikethrough 这个扩展来实现对 GFM 删除线的支持。根据扩展实现的步骤来学习下 strikethrough 扩展的源码。

**1）AST 节点结构体：Strikethrough**

```
// A Strikethrough struct represents a strikethrough of GFM text.type Strikethrough struct { gast.BaseInline}// Dump implements Node.Dump.func (n *Strikethrough) Dump(source []byte, level int) { gast.DumpHelper(n, source, level, nil, nil)}// KindStrikethrough is a NodeKind of the Strikethrough node.var KindStrikethrough = gast.NewNodeKind("Strikethrough")// Kind implements Node.Kind.func (n *Strikethrough) Kind() gast.NodeKind { return KindStrikethrough}// NewStrikethrough returns a new Strikethrough node.func NewStrikethrough() *Strikethrough { return &Strikethrough{}}
```

*   内嵌了一个 gast.BaseInline（gast 是 ast 导入时重命名的），表明是一个行级元素；
    
*   根据 goldmark 的设计，AST 节点结构体需要实现 ast.Node 接口，然而该接口拥有很多方法，为了方便实现，该库使用了内嵌的方式来处理；
    
*   ast.NewNodeKind() 构造函数得到一个 NodeKind；
    

看一下类图：

![Image 3](https://oss-emcsprod-public.modb.pro/wechatSpider/modb_20210726_8e0d04d6-edef-11eb-bf70-00163e068ecd.png)

因为 Go 不是完全面向对象语言，因此这里的类图是不严谨的：

*   BaseNode 并没有实现 Node 接口，因为它没有实现 Kind 和 Dump 方法，这也是因为 Go 没有抽象类的概念；
    
*   BaseBlock 和 BaseInline 的区别在于实现的几个方法，BaseLine 里面好几个方法直接 panic，不需要实现；
    
*   因为 BaseNode、BaseBlock 和 BaseInline 实际没有实现 Node 接口，因此它们不能直接当做 Node 使用，一定程度上模拟了抽象类；
    
*   Strikethrough 扩展通过内嵌 BaseInline “继承”了相应的实现方法，同时提供 Kind 和 Dump 的实现，达到完整实现了 Node 接口的目的，因此是一个 Node；
    

**2）Strikethrough 解析器**

```
var defaultStrikethroughDelimiterProcessor = &strikethroughDelimiterProcessor{}type strikethroughParser struct {}var defaultStrikethroughParser = &strikethroughParser{}// NewStrikethroughParser return a new InlineParser that parses// strikethrough expressions.func NewStrikethroughParser() parser.InlineParser { return defaultStrikethroughParser}func (s *strikethroughParser) Trigger() []byte { return []byte{'~'}}func (s *strikethroughParser) Parse(parent gast.Node, block text.Reader, pc parser.Context) gast.Node { before := block.PrecendingCharacter() line, segment := block.PeekLine() node := parser.ScanDelimiter(line, before, 2, defaultStrikethroughDelimiterProcessor) if node == nil {  return nil } node.Segment = segment.WithStop(segment.Start + node.OriginalLength) block.Advance(node.OriginalLength) pc.PushDelimiter(node) return node}
```

*   InlineParser 接口只有两个方法：Trigger 和 Parse；
    
*   Trigger 表示遇到什么字符触发该节点解析；
    
*   Parse 是扩展的一个关键点，不同的扩展实现方式不同。这里有两点提一下：
    

*   block.PeekLine() 获取当前行，这个很有用，解析基本都能用到；
    
*   block.Advance() 表示移动内部指针，可以理解为文件读取过程中的 Seek；
    

**3）Strikethrough 渲染器**

```
// StrikethroughHTMLRenderer is a renderer.NodeRenderer implementation that// renders Strikethrough nodes.type StrikethroughHTMLRenderer struct { html.Config}// NewStrikethroughHTMLRenderer returns a new StrikethroughHTMLRenderer.func NewStrikethroughHTMLRenderer(opts ...html.Option) renderer.NodeRenderer { r := &StrikethroughHTMLRenderer{  Config: html.NewConfig(), } for _, opt := range opts {  opt.SetHTMLOption(&r.Config) } return r}// RegisterFuncs implements renderer.NodeRenderer.RegisterFuncs.func (r *StrikethroughHTMLRenderer) RegisterFuncs(reg renderer.NodeRendererFuncRegisterer) { reg.Register(ast.KindStrikethrough, r.renderStrikethrough)}// StrikethroughAttributeFilter defines attribute names which dd elements can have.var StrikethroughAttributeFilter = html.GlobalAttributeFilterfunc (r *StrikethroughHTMLRenderer) renderStrikethrough(w util.BufWriter, source []byte, n gast.Node, entering bool) (gast.WalkStatus, error) { if entering {  if n.Attributes() != nil {   _, _ = w.WriteString("<del")   html.RenderAttributes(w, n, StrikethroughAttributeFilter)   _ = w.WriteByte('>')  } else {   _, _ = w.WriteString("<del>")  } } else {  _, _ = w.WriteString("</del>") } return gast.WalkContinue, nil}
```

*   renderer.NodeRenderer 接口只有一个方法：RegisterFuncs，用于注册节点类型对应的渲染函数；
    
*   渲染函数是一个回调函数，签名为：`func(writer util.BufWriter, source []byte, n ast.Node, entering bool) (ast.WalkStatus, error)`  
    ，用于渲染某一个节点（Node）；
    
*   渲染为 HTML，删除线通过加 `<del></del>`  
    标签来实现；
    

**4）定义一个扩展类型**

扩展需要实现 goldmark.Extender 接口。

```
type strikethrough struct {}// Strikethrough is an extension that allow you to use strikethrough expression like '~~text~~' .var Strikethrough = &strikethrough{}func (e *strikethrough) Extend(m goldmark.Markdown) { m.Parser().AddOptions(parser.WithInlineParsers(  util.Prioritized(NewStrikethroughParser(), 500), )) m.Renderer().AddOptions(renderer.WithNodeRenderers(  util.Prioritized(NewStrikethroughHTMLRenderer(), 500), ))}
```

*   这是一个固定的形式：结构体不导出，导出一个实例。外部使用时直接用导出的实例；
    
*   Extend 方法的实现，设置解析选项和渲染选项，固定的写法；
    

至此内置扩展 Strikethrough 的源码分析完成了，建议先别继续往下看，自己动手实现一个 @ 的扩展！

### Mention 扩展的实现

现在我们实现一个 @ 的扩展，命名为：Mention。

**1）AST 节点结构体：MentionNode**

```
// KindMention is a NodeKind of the Mention node.var KindMention = gast.NewNodeKind("Mention")type MentionNode struct { gast.BaseInline Who string}// NewStrikethrough returns a new Mention node.func NewMentionNode(username string) *MentionNode { return &MentionNode{  BaseInline: gast.BaseInline{},  Who:        username, }}// Dump implements Node.Dump.func (n *MentionNode) Dump(source []byte, level int) { gast.DumpHelper(n, source, level, nil, nil)}// Kind implements Node.Kind.func (n *MentionNode) Kind() gast.NodeKind { return KindMention}
```

*   这里的关键是结构体字段 Who，用于保存 @ 谁；
    
*   其他和 Strikethrough 没啥区别；
    

**2）Mention 解析器**

```
var usernameRegexp = regexp.MustCompile(`@([^\s@]{4,20})`)type mentionParser struct{}func NewMentionParser() parser.InlineParser { return mentionParser{}}func (m mentionParser) Trigger() []byte { return []byte{'@'}}func (m mentionParser) Parse(parent gast.Node, block text.Reader, pc parser.Context) gast.Node { before := block.PrecendingCharacter() if !unicode.IsSpace(before) {  return nil } line, _ := block.PeekLine() matched := usernameRegexp.FindSubmatch(line) if len(matched) < 2 {  return nil } block.Advance(len(matched[0])) node := NewMentionNode(string(matched[1])) return node}
```

*   这里假定 @ 用户名长度在 4-20 字符；
    
*   Trigger 在遇到 @ 时触发；
    
*   要求 @ 之前必须是空格；
    
*   通过正则找到当前行（line）中的目标字符串（用户名），matched 中第一个元素包含 @，第二个元素不包含 @；
    
*   因为解析出了用户名，用户名这个字符串就不需要再解析了，因此通过 block.Advance 移动指针；
    
*   构建一个 MentionNode 并返回；
    

**3）Mention 渲染器**

```
type mentionHTMLRenderer struct{}func NewMentionHTMLRenderer(opts ...html.Option) renderer.NodeRenderer { return mentionHTMLRenderer{}}func (m mentionHTMLRenderer) RegisterFuncs(reg renderer.NodeRendererFuncRegisterer) { reg.Register(KindMention, m.renderMention)}func (m mentionHTMLRenderer) renderMention(w util.BufWriter, source []byte, n gast.Node, entering bool) (gast.WalkStatus, error) { if entering {  mn := n.(*MentionNode)  w.WriteString(`<a href="https://studygolang.com/user/` + mn.Who + `">@`)  w.WriteString(mn.Who) } else {  w.WriteString("</a>") } return gast.WalkContinue, nil}
```

*   entering 为 true，表示进入该节点，因此构造链接写入 w 中；由于在 Parse 时移动了指针，因此这里将 Who 写入 w；
    
*   else 中闭合 a 标签；
    

**4）定义一个扩展类型**

```
type mention struct{}var Mention = mention{}func (m mention) Extend(markdown goldmark.Markdown) { markdown.Parser().AddOptions(parser.WithInlineParsers(  util.Prioritized(NewMentionParser(), 500), )) markdown.Renderer().AddOptions(renderer.WithNodeRenderers(  util.Prioritized(NewMentionHTMLRenderer(), 500), ))}
```

跟上面 Strikethrough 没有太多区别。

#### 使用 Mention

使用和其他扩展没有区别：

```
markdown := goldmark.New(  // 支持 GFM  goldmark.WithExtensions(extension.GFM),  // 语法高亮  goldmark.WithExtensions(    highlighting.NewHighlighting(      highlighting.WithStyle("monokai"),      highlighting.WithFormatOptions(        html.WithLineNumbers(true),      ),    ),  ),  // 支持 @  goldmark.WithExtensions(mention.Mention),)
```

这样 @ 就能正常解析了。

### 关键字方式的表情解析扩展

这个就不讲解了，有兴趣的可以动手实现下，有问题可以交流。

另外两个不错的“扩展”
-----------

另外介绍两个 goldmark “扩展”。这里扩展用引号，是因为它们并非按照上面要求的方式实现的，因此不算是真正意义上 goldmark 说的扩展，只能说是增加了 goldmark 的功能。（这也证明了 goldmark 的可扩展性很强）

### 生成目录：TOC

这是一个很实用的功能，特别对于长文来说。有一个扩展实现了该功能，即 https://github.com/mdigger/goldmark-toc。

它的实现方式是扩展 goldmark.Markdown 接口，也可以说是类似 goldmark.Extender 的方式。

```
// Markdown extends initialied goldmark.Markdown and return converter function.func Markdown(m goldmark.Markdown) ConverterFunc { m.Parser().AddOptions(  parser.WithAttribute(),  parser.WithAutoHeadingID(), ) return func(source []byte, writer io.Writer) (toc []Header, err error) {  doc := m.Parser().Parse(text.NewReader(source), WithIDs())  toc = Headers(doc, source)  if writer != nil {   err = m.Renderer().Render(writer, source, doc)  }  return toc, err }}
```

接着 Demo4，为其增加 TOC 输出，相关代码改为：

```
convertFunc := toc.Markdown(markdown)headers, err := convertFunc(source, f)for _, header := range headers {  fmt.Printf("%+v\n", header)}
```

运行输出如下信息：

```
{Level:2 Text:语法指导 ID:yu-fa-zhi-dao}{Level:3 Text:普通内容 ID:pu-tong-nei-rong}{Level:3 Text:提及用户 ID:ti-ji-yong-hu}{Level:3 Text:表情符号 Emoji ID:biao-qing-fu-hao-emoji}{Level:4 Text:一些表情例子 ID:xie-biao-qing-li-zi}{Level:3 Text:大标题 - Heading 3 ID:da-biao-ti-heading-3}{Level:4 Text:Heading 4 ID:heading-4}{Level:5 Text:Heading 5 ID:heading-5}{Level:6 Text:Heading 6 ID:heading-6}{Level:3 Text:图片 ID:tu-pian}{Level:3 Text:代码块 ID:dai-ma-kuai}{Level:4 Text:普通 ID:pu-tong}{Level:4 Text:语法高亮支持 ID:yu-fa-gao-liang-zhi-chi}{Level:5 Text:演示 Go 代码高亮 ID:yan-shi-go-dai-ma-gao-liang}{Level:5 Text:演示 JSON 代码高亮 ID:yan-shi-json-dai-ma-gao-liang}{Level:3 Text:有序、无序列表 ID:you-xu-wu-xu-lie-biao}{Level:4 Text:无序列表 ID:wu-xu-lie-biao}{Level:4 Text:有序列表 ID:you-xu-lie-biao}{Level:3 Text:表格 ID:biao-ge}{Level:3 Text:段落 ID:duan-luo}{Level:3 Text:任务列表 ID:ren-wu-lie-biao}
```

通过这些数据可以很方便的实现 TOC。

### 文本统计

这个扩展来自同一个作者：https://github.com/mdigger/goldmark-stats，用于进行文本统计，这个扩展统计的是渲染后的，因此比直接统计原始 markdown 文本要更准确。为我们 Dem4 增加统计功能，在最后加上如下代码：

```
doc := goldmark.DefaultParser().Parse(text.NewReader(source))info := stats.New(doc, source)fmt.Printf("words: %d, unique: %d, chars: %d, reading time: %v\n",  info.Words, info.Unique(), info.Chars, info.Duration(400))
```

输出：

```
words: 194, unique: 141, chars: 1263, reading time: 3m9s
```

*   作者是俄国人，这个 words 是针对西方国家的，用空格分隔的词，并非中文的字，因此中文忽略该字段；
    
*   中文主要看 chars 字段，表示多少个字；
    
*   阅读时间，我们按照一分钟 400 个字算，需要 3m9s；
    

总结
--

Markdown 已经成为程序员必须掌握的技能，如果你还不会，抓紧学习下。而这篇文章带领你从 Go 的角度对 Markdown 有了更深的了解。

希望通过 goldmark 这个库，除了学习到 Markdown 的知识，更能学习到一些 Go 语言优秀库的设计思想。

本文完整代码存放在 GitHub：https://github.com/polaris1119/go-demo/tree/master/goldmark。

* * *

觉得不错，欢迎关注：

![Image 4](https://oss-emcsprod-public.modb.pro/wechatSpider/modb_20210726_8e49a558-edef-11eb-bf70-00163e068ecd.png)

_点个赞、在看和转发是最大的支持_
