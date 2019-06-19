Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.

# Learning Git
[详细教程](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)
# Git基础 记录每次更新到仓库
## 首次配置
```
git config --global user.name "LikoLi"
git config --global user.email "likoli@aliyun.com"

# --global 全局配置, 不加这个参数则为当前项目配置
```

## 修改默认文本编辑器
```
git config --global core.editor emacs
```

## 检查配置信息
```
git config --list # 查询所有的

git config user.email # 查询 user.email 配置
```

## 获取帮助
```
git help <verb>
git <verb> --help
man git-<verb>
```

## 获取Git仓库
### 初始化一个Git仓库
```
git init
```

### 克隆现有仓库
```
git clone https://github.com/LikoLi/learngit.git

# 克隆并指令目录名
git clone https://github.com/LikoLi/learngit.git learning_git
```

## 查看Git当前状态
```
git status
git status -s/-short # 状态简览
```

## 跟踪新文件/暂存已修改的文件/将冲突文件标记为已解决
```
git add <file or dir>
```

## 忽略文件
我们可以创建一个名为 .gitignore 的文件，列出要忽略的文件模式, 来忽略我们不进行track的文件
    - 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
    - 可以使用标准的 glob 模式匹配。
    - 匹配模式可以以（/）开头防止递归。
    - 匹配模式可以以（/）结尾指定目录。
    - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 星号（\*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。 使用两个星号（\*) 表示匹配任意中间目录，比如 a/\*\*/z 可以匹配 a/z , a/b/z 或 a/b/c/z 等。

> GitHub 有一个十分详细的针对数十种项目及语言的 .gitignore 文件列表，你可以在 https://github.com/github/gitignore 找到它.

## 查看已暂存和未暂存的修改
```
git diff # 查看尚未暂存的文件更新了哪些
git diff <file or dir> # 指定查看某个文件或者目录为暂存文件的修改
git diff --cached # 查看已暂存的将要添加到下次提交里的内容
git diff --cached <file or dir> 
git diff --staged # Git 1.6.1 及更高版本, 同git diff --cached效果相同
```
> 我们使用 git diff 来分析文件差异。 但是，如果你喜欢通过图形化的方式或其它格式输出方式的话，可以使用 git difftool 命令来用 Araxis ，emerge 或 vimdiff 等软件输出 diff 分析结果。 使用 git difftool --tool-help 命令来看你的系统支持哪些 Git Diff 插件。

## 提交更新
```
git commit # 会开启默认编辑器来输入提交信息，默认的提交消息包含最后一次运行 git status 的输出，放在注释行里，另外开头还有一空行，供你输入提交说明
git commit -v # 会将你所做的改变的 diff 输出放到编辑器中从而使你知道本次提交具体做了哪些修改。
git commit -m <commit_msg> # 将提交信息和命令放在同一行，不用开启编辑器
```

## 跳过使用暂存区域
尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。 Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
```
git commit -a -m 'update README'
```

## 移除文件
```
git rm <file or dir> # 从已跟踪文件清单中移除（确切地说，是从暂存区域移除），并提交
git rm -f <file> or dir # 如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 -f（译注：即 force 的首字母）。 这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复。
git rm --cached <file or dir> # 把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中
```

## 移动文件
```
git mv file_from file_to
# git mv 命令相当于下面这三条命令
# mv file_from file_to
# git rm file_from
# git add file_to

```

# Git 基础 查看提交历史
## 查看提交历史
```
git log # 按提交时间列出所有的更新，最近的更新排在最上面
git log -p -2 # -p 用来显示每次提交的内容差异。-2 来仅显示最近两次提交
git log --stat # 显示每次提交的简略的统计信息
git log --pretty=email | format: | full | fuller | medium | oneline | raw | short
# format 以定制要显示的记录格式。 这样的输出对后期提取分析格外有用 — 因为你知道输出的格式不会随着 Git 的更新而发生改变
git log --pretty=format:"%h - %an, %ar : %s"
git log --pretty=format:"%h %s" --graph # 当 oneline 或 format 与另一个 log 选项 --graph 结合使用时尤其有用。 这个选项添加了一些ASCII字符串来形象地展示你的分支、合并历史
```

git log --pretty=format: 常用的选项

| 选项 | 说明 |
|---|---|
| %H | 提交对象（commit）的完整哈希字串 |
| %h | 提交对象的简短哈希字串 |
| %T | 树对象（tree）的完整哈希字串 |
| %t | 树对象的简短哈希字串 | 
| %P | 父对象（parent）的完整哈希字串 |
| %p | 父对象的简短哈希字串 | 
| %an | 作者（author）的名字 |
| %ae | 作者的电子邮件地址 | 
| %ad | 作者修订日期（可以用 --date= 选项定制格式） |
| %ar | 作者修订日期，按多久以前的方式显示 |
| %cn | 提交者（committer）的名字 |
| %ce | 提交者的电子邮件地址 | 
| %cd | 提交日期 |
| %cr | 提交日期，按多久以前的方式显示 |
| %s | 提交说明 |

你一定奇怪 作者 和 提交者 之间究竟有何差别， 其实作者指的是实际作出修改的人，提交者指的是最后将此工作成果提交到仓库的人。 所以，当你为某个项目发布补丁，然后某个核心成员将你的补丁并入项目时，你就是作者，而那个核心成员就是提交者。

git log 常用选项

| 选项 | 说明 |
| --- | --- |
| -p | 按补丁格式显示每个更新之间的差异。 |
| --stat | 显示每次更新的文件修改统计信息。 | 
| --shortstat | 只显示 --stat 中最后的行数修改添加移除统计。 |
| --name-only | 仅在提交信息后显示已修改的文件清单。 |
| --name-status | 显示新增、修改、删除的文件清单。 |
| --abbrev-commit | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。 |
| --relative-date | 使用较短的相对时间显示（比如，“2 weeks ago”）。 |
| --graph | 显示 ASCII 图形表示的分支合并历史。 |
| --pretty | 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。 |

## 限制输出长度
```
git log -n # 显示最近n条历史记录
git log --since=2.weeks # 列出最近2周的提交
# 上面这个命令可以在多种格式下工作，比如说具体的某一天 "2008-01-15"，或者是相对地多久以前 "2 years 1 day 3 minutes ago"

# --author 选项显示指定作者的提交
# --grep 选项搜索提交说明中的关键字。 （请注意，如果要得到同时满足这两个选项搜索条件的提交，就必须用 --all-match 选项。否则，满足任意一个条件的提交都会被匹配出来）
# -S 列出那些添加或移除了某些字符串的提交
# git log 选项是路径（path）， 如果只关心某些文件或者目录的历史提交，可以在 git log 选项的最后指定它们的路径。 因为是放在最后位置上的选项，所以用两个短划线（--）隔开之前的选项和后面限定的路径名。
```

限制git log 输出的选项

| 选项 | 说明 |
| -(n) | 仅显示最近的 n 条提交 |
| --since, --after | 仅显示指定时间之后的提交 |
| --until, --before | 仅显示指定时间之前的提交 |
| --author | 仅显示指定作者相关的提交 | 
| --committer | 仅显示指定提交者相关的提交 | 
| --grep | 仅显示含指定关键字的提交 |
| -S | 仅显示添加或移除了某个关键字的提交 |

例子: 查看 Git 仓库中，2008 年 10 月期间，Junio Hamano 提交的但未合并的测试文件
```
git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
   --before="2008-11-01" --no-merges -- t/
```

# Git 基础 撤销操作
## 撤销操作
```
git commit --amend # 将暂存区的文件合并到上一次commit中并修改提交信息
```
例子: 提交后发现忘记了暂存某些需要的修改
```
git add forgotten_file
git commit --amend

# 最终你只会有一个提交 - 第二次提交将合并到第一次提交，提交信息已第二次为准。
```

## 取消暂存的文件
```
git reset HEAD <file>... # 取消暂存
```
> 虽然在调用时加上 --hard 选项可以令 git reset 成为一个危险的命令（译注：可能导致工作目录中所有当前进度丢失！），但本例中工作目录内的文件并不会被修改。 不加选项地调用 git reset 并不危险 — 它只会修改暂存区域。

## 撤销对文件的修改
```
git checkout -- <file>... # 撤销对文件的修改
```
> 你需要知道 git checkout -- [file] 是一个危险的命令，这很重要。 你对那个文件做的任何修改都会消失 - 你只是拷贝了另一个文件来覆盖它。 除非你确实清楚不想要那个文件了，否则不要使用这个命令。

# Git 基础 - 远程仓库的使用
## 远程仓库的使用



