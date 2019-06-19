Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.

# Learning Git

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
所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。 星号（*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）。 使用两个星号（*) 表示匹配任意中间目录，比如 a/**/z 可以匹配 a/z , a/b/z 或 a/b/c/z 等。




