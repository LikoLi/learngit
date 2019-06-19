Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.

# Learning Git

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
| --- | --- |
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
