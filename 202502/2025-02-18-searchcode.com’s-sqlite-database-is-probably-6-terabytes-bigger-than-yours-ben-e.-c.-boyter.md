# searchcode.com’s SQLite database is probably 6 terabytes bigger than yours | Ben E. C. Boyter
- URL: https://boyter.org/posts/searchcode-bigger-sqlite-than-you/
- Added At: 2025-02-18 00:15:56
- [Link To Text](2025-02-18-searchcode.com’s-sqlite-database-is-probably-6-terabytes-bigger-than-yours-ben-e.-c.-boyter_raw.md)

## TL;DR
searchcode.com成功将其6.4TB的数据库从MySQL迁移到SQLite，展示了SQLite在大规模应用中的潜力。通过技术栈的迭代和硬件升级，项目实现了性能显著提升，并计划进一步扩大规模和探索新的代码托管平台。

## Summary
1. **SQLite数据库规模**：
   - searchcode.com的SQLite数据库规模为6.4TB，可能是世界上最大的公开SQLite数据库之一。
   - 作者未发现更大的公开SQLite数据库，最大的公开记录为1TB。

2. **searchcode.com项目背景**：
   - searchcode.com是一个源代码搜索引擎，支持多种代码托管平台和300多种编程语言。
   - 项目经历了多次技术栈的迭代和重构，从最初的PHP、MySQL到现在的Go、SQLite。

3. **技术栈演变**：
   - 初始版本：PHP、CodeIgniter、MySQL、Memcached、Apache2、Sphinx搜索。
   - 中间版本：Python、Django、MySQL、Memcached、Sphinx搜索、Nginx、RabbitMQ。
   - 未发布版本：Java、MySQL、Memcached、Nginx、Sphinx搜索。
   - 疫情期间版本：Go、MySQL、Redis、Caddy、Manticore搜索。
   - 当前版本：Go、SQLite、Caddy。

4. **选择SQLite的原因**：
   - 减少依赖，实现单二进制部署。
   - SQLite可以直接编译进二进制文件，无需安装额外依赖。
   - 作者不自信能自己编写存储持久层，选择使用SQLite。

5. **SQLite使用中的挑战**：
   - 遇到“database is locked”错误，通过设置两个连接（一个用于读取，一个用于写入）解决。
   - 跨平台编译问题，使用纯Go版本的SQLite解决。

6. **数据库迁移**：
   - 从MySQL迁移到SQLite，使用SQLC工具提高数据库访问效率。
   - 数据压缩问题，最终选择在文件系统层面使用BTRFS和zstd压缩。

7. **硬件升级**：
   - 从AMD 5950x升级到Intel Xeon Gold 5412U，增加RAM和更快磁盘。
   - 新硬件支持更大的索引和更低的误报率。

8. **迁移结果**：
   - 迁移后性能提升，搜索和页面加载速度更快。
   - 索引过程顺利进行，48核心充分利用。

9. **未来计划**：
   - 扩大searchcode.com的规模，实现盈利。
   - 探索索引其他代码托管平台的可能性。

10. **总结**：
    - searchcode.com的SQLite数据库迁移是一个成功的案例，展示了SQLite在大规模应用中的潜力。
    - 通过技术栈的不断优化和硬件的升级，searchcode.com实现了性能的显著提升。
