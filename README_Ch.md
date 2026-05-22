# Shell Scripting 中文学习指南

这是 `shell-scripting-tutorial` 仓库的中文学习入口。仓库内容围绕 Bash / Shell 脚本展开，适合从零开始学习 Linux 命令行自动化，也适合已有 Linux 基础的同学用来查漏补缺。

原仓库主要资料位于 [`Tutorial-Files`](Tutorial-Files) 目录中，内容以 Markdown 文档为主，不需要安装依赖，也不需要启动服务。克隆到本地后，直接用 VS Code、Typora、Obsidian 或 GitHub 页面阅读即可。

## 适合谁学习

- 刚开始学习 Linux、Shell、Bash 的初学者。
- 想用脚本自动化日常任务的学生、工程师或运维人员。
- 想系统复习变量、条件判断、循环、函数、数组、文件处理、正则表达式等 Shell 基础的人。
- 正在学习超算、服务器、集群环境，希望提升命令行效率的人。

## 学习前准备

建议你先具备以下环境：

- 一台 macOS、Linux 或带有 WSL 的 Windows 电脑。
- 一个可用的终端，例如 Terminal、iTerm2、Windows Terminal。
- 基本的 Git 使用能力，例如 `clone`、`status`、`pull`。
- 一个文本编辑器，推荐 VS Code。

进入本地仓库：

```bash
cd "/Users/yunfan/Linux与超算学习/shell-scripting-tutorial"
```

查看当前 Bash 版本：

```bash
bash --version
```

如果你在 macOS 上，默认 shell 可能是 `zsh`。大多数基础命令仍然通用，但学习 Bash 脚本时，建议在脚本开头使用：

```bash
#!/usr/bin/env bash
```

## 推荐学习顺序

建议按下面顺序学习，每学完一个主题，就自己写一个小脚本练习。Shell 脚本很重实践，只读不敲很容易“看懂了但不会写”。

1. 先读 Linux 速查表，熟悉常用命令。
2. 学 Bash 基础，理解 Shell、终端、脚本之间的关系。
3. 学文件和权限，这是后续脚本操作的基础。
4. 学变量、字符串、数字运算。
5. 学条件判断、循环和函数。
6. 学数组、文件处理、管道和重定向。
7. 学正则、`grep`、`sed`、`awk`。
8. 学错误处理、环境变量、调试技巧。
9. 最后看进程管理、定时任务、安全实践和真实案例。

## 目录导航

### 快速参考

- [Linux 命令速查表（中文）](Tutorial-Files/Linux-cheat-sheet_Ch.md)
- [Linux 命令速查表（英文原版）](Tutorial-Files/Linux-cheat-sheet.md)
- [补充速查表](cheatsheet-18.md)

### 1. Bash 入门

- [什么是 Bash](<Tutorial-Files/01.Introduction-to-Bash/01.What is Bash.md>)
- [Shell 脚本在自动化中的重要性](<Tutorial-Files/01.Introduction-to-Bash/02.Importance of shell scripting in automation.md>)

### 2. 基础命令

- [常用基础命令：ls、cd、mkdir、rm、cp、mv 等](Tutorial-Files/02.Basic-Commands/01.Basic_Commands.md)
- [理解文件权限：chmod、chown](Tutorial-Files/02.Basic-Commands/02.Understanding_file_permissions.md)

### 3. 变量与数据类型

- [声明和使用变量](Tutorial-Files/03.Variables-and-Data-Types/01.Declaring_and_using_variables.md)
- [字符串处理](Tutorial-Files/03.Variables-and-Data-Types/02.String_manipulation.md)
- [数字运算](Tutorial-Files/03.Variables-and-Data-Types/03.Numeric_Operations.md)

### 4. 条件语句

- [`if`、`elif`、`else` 语句](Tutorial-Files/04.Conditional-Statements/01.if_elif_else_statements.md)
- [`case` 语句](Tutorial-Files/04.Conditional-Statements/02.Case_statements.md)

### 5. 循环

- [`for`、`while`、`until` 循环](Tutorial-Files/05.Loops/01.for_while_until_loops.md)
- [循环控制：break、continue](<Tutorial-Files/05.Loops/02.Loop_control statements_(break, continue).md>)

### 6. 函数

- [定义和使用函数](Tutorial-Files/06.Functions/01.Defining_and_using_functions.md)
- [向函数传递参数](Tutorial-Files/06.Functions/02.Passing_arguments_to_functions.md)
- [从函数返回值](Tutorial-Files/06.Functions/03.Returning_values_from_functions.md)

### 7. 数组

- [声明和访问数组](Tutorial-Files/07.Arrays/01.Declaring_and_accessing_arrays.md)
- [数组操作](Tutorial-Files/07.Arrays/02.Array_manipulation.md)

### 8. 文件处理

- [读取文件与写入文件](Tutorial-Files/08.File-Handling/01.Reading_from_and_writing_to_files.md)
- [检查文件是否存在及文件类型](Tutorial-Files/08.File-Handling/02.Checking_file_existence_and_type.md)
- [文件处理命令：sed、awk](<Tutorial-Files/08.File-Handling/03.File_manipulation_commands_(sed, awk).md>)

### 9. 输入输出重定向

- [标准输入与标准输出重定向](Tutorial-Files/09.Input_Output-Redirection/01.Redirecting_standard_input_and_output.md)
- [使用管道串联命令](Tutorial-Files/09.Input_Output-Redirection/02.Using_pipes_for_command_chaining.md)

### 10. 正则表达式

- [基础正则表达式模式](Tutorial-Files/10.Regular-Expressions/01.Basic_regex_patterns.md)
- [`grep`、`sed`、`awk` 模式匹配与文本处理](<Tutorial-Files/10.Regular-Expressions/02.grep, sed, and awk for pattern matching and text processing.md>)

### 11. 错误处理

- [使用退出码处理错误](Tutorial-Files/11.Error-Handling/01.Handling_errors_with_exit_codes.md)
- [使用 trap 处理信号](Tutorial-Files/11.Error-Handling/02.Using_trap_for_signal_handling.md)

### 12. 环境变量

- [内置环境变量](Tutorial-Files/12.Environment-Variables/01.Built-in_environment_variables.md)
- [自定义环境变量](Tutorial-Files/12.Environment-Variables/02.Custom_environment_variables.md)

### 13. 调试技巧

- [使用 echo 和 printf 调试](Tutorial-Files/13.Debugging-Techniques/01.Using_echo_and_printf_for_debugging.md)
- [设置和使用断点](Tutorial-Files/13.Debugging-Techniques/02.Setting_and_using_breakpoints.md)

### 14. 高级脚本技术

- [管理进程：ps、kill、jobs](<Tutorial-Files/14.Advanced-Scripting-Techniques/01.Managing_processes (ps, kill, jobs).md>)
- [使用 cron 定时执行任务](Tutorial-Files/14.Advanced-Scripting-Techniques/02.Job_scheduling_with_cron.md)
- [信号处理](Tutorial-Files/14.Advanced-Scripting-Techniques/03.Signal_handling.md)

### 15. 安全最佳实践

- [编写安全的脚本](Tutorial-Files/15.Security-Best-Practices/01.Writing_secure_scripts.md)
- [避免常见脚本陷阱](Tutorial-Files/15.Security-Best-Practices/02.Avoiding_common_pitfalls.md)

### 16. 与外部命令交互

- [在脚本中运行外部命令](<Tutorial-Files/16.Interacting-with-External-Commands/01.Running external commands from scripts.md>)
- [捕获并使用命令输出](<Tutorial-Files/16.Interacting-with-External-Commands/02.Capturing and using command output.md>)

### 17. 真实案例

- [常见任务脚本：日志分析、数据处理、系统监控](<Tutorial-Files/17.Real-world-Examples/01.Practical scripts for common tasks (log analysis, data processing, system monitoring).md>)
- [与其他工具和技术集成](<Tutorial-Files/17.Real-world-Examples/02.Integration with other tools and technologies.md>)

### 18. 最佳实践

- [编码规范](<Tutorial-Files/19.Best-Practices/01.Coding standards.md>)
- [代码审查与协作](<Tutorial-Files/19.Best-Practices/02.Code reviews and collaboration.md>)

### 19. 总结

- [课程总结](Tutorial-Files/19.Conclusion.md)

## 本地练习建议

你可以在仓库根目录下新建一个自己的练习目录，例如：

```bash
mkdir my-practice
cd my-practice
```

创建第一个脚本：

```bash
touch hello.sh
chmod +x hello.sh
```

示例内容：

```bash
#!/usr/bin/env bash

name="Shell"
echo "Hello, ${name}!"
```

运行：

```bash
./hello.sh
```

## 推荐练习题

- 写一个脚本，输出当前日期、当前用户、当前目录。
- 写一个脚本，判断某个文件是否存在。
- 写一个脚本，批量创建 `lesson01` 到 `lesson10` 文件夹。
- 写一个脚本，统计某个日志文件中包含 `error` 的行数。
- 写一个脚本，接收一个目录路径，列出其中最大的 5 个文件。
- 写一个脚本，使用函数封装重复逻辑。
- 写一个脚本，使用 `trap` 在退出前清理临时文件。

## 常用命令备忘

```bash
# 查看仓库状态
git status

# 拉取你的 fork 上的最新内容
git pull

# 搜索教程中的关键词
rg "keyword" Tutorial-Files

# 查看某个脚本的语法是否有明显错误
bash -n script.sh

# 以调试模式运行脚本
bash -x script.sh
```

## 关于本仓库

本仓库 fork 自开源 Shell 脚本教程项目，原始内容版权和许可证请参考：

- [LICENSE](LICENSE)
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [SECURITY.md](SECURITY.md)

这个中文 README 主要用于本地学习导航，并没有替换原始英文资料。建议学习时保留英文术语，例如 `variable`、`loop`、`function`、`pipe`、`redirection`，这样以后阅读官方文档和命令帮助会更顺畅。
