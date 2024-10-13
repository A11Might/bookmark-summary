# 专为 Gopher 准备的 Markdown 教程 - 墨天轮
- URL: https://www.modb.pro/db/87166
- Added At: 2024-10-13 14:50:25
- [Link To Text](2024-10-13-专为-gopher-准备的-markdown-教程---墨天轮_raw.md)

## TL;DR
本文通过Go语言的goldmark库深入探讨Markdown，介绍了CommonMark和GFM标准，详细讲解了goldmark的使用、设计和扩展实现，展示了如何通过Go语言掌握Markdown并学习优秀库的设计思想。

## Summary
1. **Markdown简介**：
   - Markdown是程序员必须掌握的技能，广泛应用于各种社区。
   - 本文不是Markdown语法教程，而是通过Go语言Markdown解析库的学习来深入了解Markdown。

2. **CommonMark和GFM**：
   - **CommonMark**：
     - 是Markdown的标准或规范，旨在消除Markdown解析渲染的二义性。
     - 主要参与者包括来自Meteor、GitHub、Reddit、Stack Exchange和Discourse的开发者。
   - **GFM**：
     - GitHub Flavored Markdown，基于标准Markdown增加了一些功能。
     - 由于GitHub的流行，GFM几乎成为最强大的Markdown衍生分支。

3. **Go语言Markdown解析器**：
   - **选择解析器**：
     - 根据Star数和规范推荐选择解析器。
     - `russross/blackfriday`是最早的Go语言Markdown解析库，但不兼容CommonMark。
     - `yuin/goldmark`是Hugo默认的Markdown解析器，兼容CommonMark 0.29规范。
   - **goldmark简介**：
     - 易于扩展、符合标准、结构良好。
     - 特性包括符合CommonMark规范、可扩展性、性能、健壮性、内置扩展、只依赖标准库。

4. **goldmark的使用**：
   - **安装goldmark**：
     - 使用Go Module安装goldmark。
   - **Demo示例**：
     - **Demo1**：基本转换，存在不支持自动链接、删除线、表格、任务列表、语法高亮、@和表情等问题。
     - **Demo2**：通过goldmark内置的GFM扩展解决部分问题。
     - **Demo3**：通过goldmark-highlighting扩展解决语法高亮问题。

5. **goldmark的设计**：
   - **Markdown接口**：
     - 包含解析器、渲染器、解析markdown文本并渲染结果的方法。
   - **Option模式**：
     - 通过Option函数类型控制Markdown的行为。
   - **Extender接口**：
     - 用于扩展Markdown，方法接收一个Markdown参数。

6. **自己实现一个goldmark扩展**：
   - **扩展实现步骤**：
     - 定义AST节点结构体。
     - 定义解析器。
     - 定义渲染器。
     - 定义goldmark扩展。
   - **示例：Mention扩展**：
     - 实现@用户名的解析和渲染。

7. **其他goldmark扩展**：
   - **TOC扩展**：生成目录。
   - **文本统计扩展**：进行文本统计，输出字数、字符数和阅读时间。

8. **总结**：
   - Markdown已成为程序员必须掌握的技能。
   - 通过goldmark库学习Markdown，同时学习Go语言优秀库的设计思想。
