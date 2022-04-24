# .gitignore

Recommend Reading:

[忽略特殊文件 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)

[gitignore文件屏蔽规则 - 简书 (jianshu.com)](https://www.jianshu.com/p/13612fb4b224)

[Git - Recording Changes to the Repository (git-scm.com)](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_ignoring)

## 原则

> 1. 忽略操作系统自动生成的文件，比如缩略图等；
> 2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的`.class`文件；
> 3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

## 规则

- 所有空行或#开头的行都会被忽略；
- 可以使用标准的**glob模式**匹配；

### glob模式

- 文件或目录前加 `/` 表示仓库根目录的对应文件；否则匹配相对于当前 .gitignore 文件路径的内容

- 匹配模式最后跟反斜杠 `/` 说明要忽略的是目录；

- 以星号"*"通配多个字符，即匹配多个任意字符；使用两个星号"**" 表示匹配任意中间目录，比如`a/**/z`可以匹配 a/z, a/b/z 或 a/b/c/z等。

  **注意**：glob与正则表达式虽然非常相似，但是还是有不一样。比如a*k在glob中可以匹配ak,abk,abck，但在正则表示中表示匹配ak,aak,aaak。

- 以问号"?"通配单个字符，即匹配一个任意字符；

- 要特殊不忽略某个文件或目录，可以在模式前加上取反 `!` 

  ```bash
  readme.md       # 屏蔽仓库中所有名为 readme.md 的文件
  !/readme.md     # 在上一条屏蔽规则的条件下，不屏蔽仓库根目录下的 readme.md 文件
  ```

  **注意**：顺序很重要，必须要先屏蔽所有的，然后才建立特殊不屏蔽的规则！

### 使用例

```
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

