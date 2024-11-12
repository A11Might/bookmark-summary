# Shae Erisson 的博客 - 我的同事要求我不要编写的 github 插件。 --- Shae Erisson's blog - The github plugin my coworkers asked me not to write.
- URL: https://www.scannedinavian.com/the-github-plugin-my-coworkers-asked-me-not-to-write.html
- Added At: 2024-11-12 00:26:44
- [Link To Text](2024-11-12-shae-erisson-的博客---我的同事要求我不要编写的-github-插件。-----shae-erisson's-blog---the-github-plugin-my-coworkers-asked-me-not-to-write._raw.md)

## TL;DR
作者Shae Erisson与[<mclare\>](https://mclare.blog/)合作，研究了GitHub项目的Bus Factor，发现Linux内核的Truck Factor从2015年的90降至8，表明项目依赖性增加。他们通过复现研究，解决了技术问题，并计划改进计算方法。

## Summary
1. **博客背景**：
   - 博客由Shae Erisson和[<mclare\>](https://mclare.blog/)共同撰写，后者负责制作博客末尾的酷炫可视化图表。

2. **Bus Factor/Truck Factor定义**：
   - 根据维基百科，“Bus Factor”或“Truck Factor”是指项目中必须突然消失的最少团队成员数，以至项目因缺乏知识或合格人员而停滞。

3. **动机**：
   - 2015年，作者的雇主进行了裁员，其中一位被裁员工是公司某部分代码库的唯一贡献者，该代码库为公司带来收入。作者因此想编写一个GitHub企业插件，计算哪些员工不能被解雇。

4. **插件开发**：
   - 作者开始编写插件，并在周四下午的闪电演讲中讨论了五分钟。同事们认为这会立即触发Goodhart定律，即管理团队可能会利用此插件计算哪些员工可以被解雇。

5. **研究背景**：
   - 原始研究计算了多个流行GitHub项目（包括Linux内核）的Truck Factor，最初预印本中指出，Linux项目需要80人离开才能停止。

6. **复现研究**：
   - 作者和[<mclare\>](https://mclare.blog/)决定复现研究结果，查看过去十年中Truck Factor是否有所改善。
   - 研究论文的GitHub仓库仍然可用，数据以JSON格式提供，可视化图表基于CSV文件。

7. **复现过程**：
   - 作者和[<mclare\>](https://mclare.blog/)遇到了一些技术问题，如README指令不完整，GNU Parallel使用问题，以及在NixOS上安装Ruby Gems的困难。
   - 他们最终通过GNU Parallel并行克隆了所有GitHub仓库，并重新计算了Truck Factor。

8. **结果分析**：
   - 重新计算的结果显示，Linux内核的Truck Factor为12，而原始研究中为80。
   - 未使用Linguist插件过滤文档和第三方库时，Truck Factor为12；使用插件后，Truck Factor降至8。

9. **问题与改进**：
   - 计算未考虑代码审查过程，且未使用Levenshtein距离合并开发者别名。
   - 未来工作包括改进计算方法，考虑Git的co-authored-by和reviewer头信息，以及比较当前流行项目与历史数据。

10. **结论**：
    - 结论是Bus Factor变得更糟，Linux内核的Truck Factor从2015年的90降至目前的8。

11. **可视化**：
    - 更多可视化内容和细节，请查看[<mclare\>](https://mclare.blog/)的博客。
