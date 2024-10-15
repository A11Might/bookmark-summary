# How I Built My Blog • Josh W. Comeau
- URL: https://www.joshwcomeau.com/blog/how-i-built-my-blog-v2/
- Added At: 2024-10-15 02:37:58
- [Link To Text](2024-10-15-how-i-built-my-blog-•-josh-w.-comeau_raw.md)

## TL;DR
作者更新了博客，采用MDX和Next.js技术栈，设计更精致，使用Linaria样式和Shiki语法高亮。增加了交互式代码游乐场和搜索功能，注重可访问性，并从Pages Router切换到App Router。

## Summary
1. **博客更新**：过去几个月，作者一直在开发博客的新版本，并于几周前正式上线。

2. **设计变化**：
   - **旧版博客**：展示了旧版博客的暗模式和亮模式截图。
   - **新版博客**：展示了新版博客的暗模式和亮模式截图。
   - **设计改进**：新版博客在设计上更加精致，但整体概念保持不变。

3. **技术栈**：
   - **核心技术**：列出了博客使用的主要技术，包括MDX、Next.js等。
   - **技术选择原因**：
     1. 所有博客文章使用MDX编写，需要一流的MDX支持。
     2. 作者的其他主要项目使用Next.js，希望减少上下文切换的摩擦。
     3. 希望获得更多React最新特性的经验，如Server Components和Actions。

4. **内容管理**：
   - **MDX使用**：博客文章使用MDX编写，这是技术栈中最关键的部分。
   - **MDX优势**：MDX结合了Markdown和JSX，允许在内容中包含自定义React元素，增强了内容的交互性。
   - **工作流程**：在VS Code中直接编辑MDX文件，并将其作为代码提交。文章元数据（如标题、发布日期）在文件顶部的frontmatter中设置。

5. **样式和CSS**：
   - **旧版样式**：使用styled-components。
   - **新版样式**：切换到Linaria，通过next-with-linaria集成。
   - **Linaria优势**：提供熟悉的`styled` API，但编译为CSS模块，无JS运行时，完全兼容React Server Components。
   - **Linaria挑战**：在Next.js中使用Linaria遇到一些问题，如TextEncoder未定义错误。
   - **未来计划**：计划在Pigment CSS发布1.0版本后切换到该库。

6. **代码片段**：
   - **旧版代码片段**：展示了旧版代码片段的截图。
   - **新版代码片段**：展示了新版代码片段的截图，使用了自定义设计的语法主题。
   - **Shiki使用**：使用Shiki进行语法高亮，支持多种语言，无额外JavaScript包大小。
   - **Shiki挑战**：Shiki内存消耗大，可能导致Node内存不足，需要优化。

7. **代码游乐场**：
   - **React游乐场**：使用Sandpack，一个由CodeSandbox团队创建的编辑器。
   - **静态HTML/CSS游乐场**：使用agneym的Playground的fork。
   - **交互式演示**：使用React Spring和Framer Motion进行动画处理。

8. **数据库**：
   - **点赞按钮**：每个访客最多可以点击16次，数据存储在MongoDB中。
   - **用户ID**：基于用户IP地址生成，使用秘密盐进行哈希以保护匿名性。

9. **细节设计**：
   - **元素内聚性**：花费大量时间确保通用组件组合良好，如`<Aside>`和`<CodeSnippet>`组件的组合。
   - **彩虹效果**：桌面主页上的彩虹效果，使用PartyKit实现实时广播。
   - **视图过渡**：使用View Transitions API实现页面导航时的过渡动画。
   - **搜索功能**：使用Algolia实现搜索功能，点击垃圾桶图标可以逐字清除搜索词。

10. **现代轮廓图标**：
    - **图标改进**：图标经过微调，增加了微交互。
    - **图标制作**：从Feather Icons开始，然后分解或重建SVG以实现动画。

11. **可访问性**：
    - **媒体查询**：使用rem单位进行媒体查询，确保布局适应用户浏览器默认字体大小。
    - **持续学习**：作者不断学习可访问性知识，并应用于新博客。

12. **App Router vs. Pages Router**：
    - **切换原因**：从Pages Router切换到App Router，体验好坏参半。
    - **优点**：Server Components范式更自然，更强大的服务器端工作能力。
    - **缺点**：开发服务器速度较慢，性能略差。
    - **未来展望**：Next.js团队正在优先解决开发性能问题，App Router仍处于早期阶段。

13. **基础构建**：
    - **教学经验**：作者教授React已有7年，创建了The Joy of React课程。
    - **课程项目**：课程的最终项目是一个交互式MDX博客，可以作为实际博客的基础。
