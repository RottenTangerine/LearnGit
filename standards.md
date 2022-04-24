# Standards

## commit message规范

[How to Write a Git Commit Message (cbea.ms)](https://cbea.ms/git-commit/)

[git commit 规范指南 - 简书](https://www.jianshu.com/p/201bd81e7dc9)

#### Breaking Change

以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

#### Closed Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue

```
Closes #234
```

#### Revert

以revert:开头，后面跟着被撤销 Commit 的 Header

Body部分的格式是固定的，必须写成`This reverts commit <hash>`.，其中的hash是被撤销 commit 的 SHA 标识符。

```
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。