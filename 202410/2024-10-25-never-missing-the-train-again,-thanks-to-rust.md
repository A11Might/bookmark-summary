# Never Missing the Train Again, Thanks to Rust
- URL: https://lilymara.xyz/posts/2024/01/transit-kindle/
- Added At: 2024-10-25 00:53:38
- [Link To Text](2024-10-25-never-missing-the-train-again,-thanks-to-rust_raw.md)

## TL;DR
作者利用旧Kindle设备显示实时交通信息，通过越狱、图像处理、数据获取和UI优化，构建了一个显示公交到达时间的系统，最终使用Rust和Skia实现高效图像生成和HTTP服务。

## Summary
1. **项目背景**：
   - 作者生活在旧金山，依赖公共交通出行。
   - 现有的公共交通应用通常提供全程导航，不适合已熟悉路线的用户。
   - 作者希望有一个显示附近公交/火车/电车等交通工具到达时间的简单工具。

2. **灵感来源**：
   - 受到Matt Healy和Ben Borgers的启发，决定利用旧Kindle设备显示实时交通信息。

3. **Kindle越狱**：
   - 第一步是对Kindle进行越狱，以启用USBNet功能，从而可以通过SSH访问Kindle并设置cron任务更新显示。

4. **在Kindle上显示图像**：
   - 尝试在Kindle上显示图像，发现图像显示时会拉伸变形。
   - 通过创建校准图像，发现Kindle仅支持8位PNG图像，最终使用ImageMagick的`convert`工具将截图转换为8位PNG图像。

5. **生成有用图像**：
   - 目标是生成包含实时交通到达时间的图像，而不是一次性显示。
   - 使用Node.js服务器和Puppeteer截取BART页面的一部分，调整大小和颜色深度后通过HTTP端点返回。
   - 设置Kindle每分钟通过cron任务获取图像。

6. **扩展到MUNI**：
   - 旧金山有27个公共交通运营商，作者希望增加MUNI的到达时间显示。
   - 尝试通过Puppeteer截取多个MUNI站点的状态页面，但由于内存和API速率限制问题，系统变得不稳定。

7. **重新设计架构**：
   - 决定使用Rust和Axum构建新的HTTP服务器，放弃Puppeteer。
   - 使用511.org的Stop Monitoring API获取实时到达时间数据。
   - 使用Skia图形库直接渲染PNG图像，减少资源消耗。

8. **获取数据**：
   - 通过511.org API获取MUNI和BART的实时到达时间数据，并解析JSON响应。
   - 过滤出关心的站点数据，并按线路和方向组织数据。

9. **使用Skia构建PNG**：
   - 学习Skia的基本用法，创建一个简单的“Hello World”PNG图像。
   - 使用Skia渲染包含公交到达时间的表格图像，逐步优化布局和显示效果。

10. **通过Axum提供PNG**：
    - 使用Axum构建HTTP服务器，提供生成的PNG图像。
    - 调整图像生成代码，使其在内存中生成PNG数据并返回给HTTP响应。

11. **UI优化**：
    - 进一步优化图像布局，添加列标题、圆角矩形背景、时间戳和数据缓存状态等元素。
    - 最终版本包括反锯齿、不同灰度颜色区分线路、目的地名称过长时的渐变裁剪等功能。

12. **总结**：
    - 项目从最初的BART截图显示发展到使用Rust和Skia构建的完整系统。
    - 详细介绍了从数据获取、图像生成到HTTP服务器的构建过程。
    - 提供了最终代码的GitHub链接，并鼓励读者通过捐款支持相关组织。
