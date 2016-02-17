#写出好的 commit message

##为什幺要关注提交信息

* 加快 Reviewing Code 的过程
* 帮助我们写好 release note
* 5年后帮你快速想起来某个分支，tag 或者 commit 增加了什么功能，改变了哪些代码
* 让其他的开发者在运行 git blame 的时候想跪谢
* 总之一个好的提交信息，会帮助你提高项目的整体质量

## commit_message_change_log
Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。

格式： <type>(<scope>): <subject>

例如： feat(login): 登录相关逻辑

###（1）type
* type用于说明 commit 的类别，只允许使用下面7个标识。
* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动

如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。
###（2）scope
scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。
###（3）subject
* subject是 commit 目的的简短描述，不超过50个字符。
* 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
* 第一个字母小写
* 结尾不加句号（.）


=========old

## 基本要求
* 第一行应该少于50个字。 随后是一个空行 第一行题目也可以写成：Fix issue #8976
* 使用 fix（修复bug）, add（添加功能）, change（调整代码等） 而不是 fixed, added, changed
* 请将每次提交限定于完成一次逻辑功能。并且可能的话，适当地分解为多次小更新，以便每次小型提交都更易于理解。

## 例子

```
Fix issue #9527 message

小改直接就用一句话说清楚。
大改的，自己建一个 Issue 说清楚情况、方案、变化。。。。
其实最重要一点，commit log 是给人类看的，说清楚就好，不必太过拘谨，更不能写成只给机器看的东西。

```
或者

```
Add feature #9527 message
```
