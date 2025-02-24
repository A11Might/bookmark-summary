# Oh Shit, Git!?!
- URL: https://ohshitgit.com/
- Added At: 2025-01-17 00:20:21
- [Link To Text](2025-01-17-oh-shit,-git!-!_raw.md)

## TL;DR
文章总结了Git使用中的常见问题及其解决方案，包括如何撤销提交、修改提交信息、处理错误提交等。同时提供了极端情况下的处理方法，如重置仓库或删除本地仓库。文章还鼓励用户参与翻译贡献，并感谢了现有的翻译贡献者。

## Summary
1. **Git的挑战**：
   - Git操作复杂，容易出错，且修复错误的过程往往困难重重。
   - Git文档存在“鸡与蛋”的问题，即除非你已知道需要了解的内容，否则难以搜索到解决问题的方法。

2. **常见问题及解决方案**：
   - **时间机器功能**：
     - 使用`git reflog`查看所有操作记录，通过`git reset HEAD@{index}`回退到错误发生前的状态。
   - **修改最后一次提交**：
     - 修改文件后，使用`git commit --amend --no-edit`将更改合并到上次提交中。
   - **更改提交信息**：
     - 使用`git commit --amend`修改最后一次提交的信息。
   - **错误提交到主分支**：
     - 创建新分支保存当前状态，然后使用`git reset HEAD~ --hard`从主分支移除最后一次提交。
   - **提交到错误分支**：
     - 使用`git reset HEAD~ --soft`撤销提交但保留更改，然后切换到正确分支并重新提交。
   - **diff无输出**：
     - 使用`git diff --staged`查看已暂存文件的差异。
   - **撤销旧提交**：
     - 使用`git log`找到提交的哈希值，然后使用`git revert [hash]`撤销该提交。
   - **撤销文件更改**：
     - 使用`git checkout [hash] -- path/to/file`恢复文件到指定提交的状态。

3. **极端情况处理**：
   - **完全放弃**：
     - 使用`sudo rm -r`删除本地仓库，然后重新克隆。
   - **重置仓库状态**：
     - 使用`git fetch origin`和`git reset --hard origin/master`将本地仓库重置为远程仓库的状态。

4. **免责声明与感谢**：
   - 该网站并非详尽无遗的参考，提供的方法基于作者的经验和试错。
   - 感谢所有自愿将网站翻译成其他语言的贡献者。

5. **贡献与翻译**：
   - 鼓励用户通过GitHub提交PR，帮助添加新的语言翻译。
