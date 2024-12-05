# A Made-up Name is Better Than No Name | Marcus' Blog
- URL: https://mbuffett.com/posts/a-made-up-name/
- Added At: 2024-12-05 00:19:25
- [Link To Text](2024-12-05-a-made-up-name-is-better-than-no-name-marcus'-blog_raw.md)

## TL;DR
作者在开发Chessbook时，为简化处理(position, move)对，自创了名称`Kep`，用于表示EPD和San的组合。这一命名简化了代码和思考过程，作者认为自创名称是一个有用的工具，建议适度使用。

## Summary
1. **背景**：
   - 在开发Chessbook时，作者经常需要处理(position, move)对，具体来说，位置存储为EPD格式，移动存储为San符号。

2. **代码示例**：
   - 原始代码中使用`(epd, san_plus)`对来表示位置和移动。
   - 示例代码：
     ```rust
     let difficulty_by_epd_san = //...;
     let existing_epd_sans = //...;
     let unique_moves_by_epd_san = //...;
     fn epd_san_plus_to_condition((epd, san_plus): &(String, String)) -> _ //...;
     ```

3. **命名需求**：
   - 作者习惯于将这些对视为一个整体，并希望为其命名。
   - 找不到合适的现有名称，如`MoveFromPosition`过于冗长。

4. **自创名称**：
   - 作者创造了一个新名称`Kep`，用于表示EPD和San的组合。
   - 新名称的使用简化了代码：
     ```rust
     let difficulty_by_kep = //...;
     let existing_keps = //...;
     let unique_moves_by_kep = //...;
     fn kep_to_condition((epd, san_plus): &Kep) -> _ //...;
     ```

5. **命名的好处**：
   - 命名后，思考和处理这些对变得更简单。
   - `(epd, san_plus)`对占用两个工作记忆槽，而`Kep`只占用一个。

6. **总结**：
   - 作者认为自创名称是一个有用的工具，可以简化思考和代码编写。
   - 建议适度使用，但认为这是一个值得添加到工具箱中的技巧。

7. **联系方式**：
   - 作者欢迎通过电子邮件或Twitter联系。
   - 提供PSN账号和Chessbook项目链接。
   - 提及女友的播客项目。
   - 提供赞助链接。
