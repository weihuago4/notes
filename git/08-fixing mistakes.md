# 08-FIX MISTAKES

## 8.1`GIT CHECKOUT`

`git checkout`可以**从工作树(working tree)中恢复文件**或者**切换到不同的分支**.

![](images/git_checkout.png)

### 使用`git checkout <branch>` 会发生什么?

- Git会将**HEAD**指向到新的分支
- 从**仓库(Repo)**中拷贝该分支所指向的commit快照放入**暂存区域(Staging Area)**中
- 使用**当前HEAD指向分支**的内容替换**工作区域的内容**

![](images/checkout_a_branch.png)

### 使用`git checkout -- <file>`会发生什么?

Git会使用**当前暂存区域的内容替换工作区域中的内容**.

**注意:**此操作会完全将工作区域的内容替换掉,你得不到Git的任何提示.

![](images/checkout_file.png)

### 对一个特定的commit使用`git checkout <commit>  -- file`会发生什么?

- 更新**暂存区域的内容**为该**特定的commit的快照**
- 根据**暂存区域**的commit快照更新**工作区域的内容**

![](images/checkout_file_from_commit.png)

**注意:**此操作同样也不会被Git所警告.

- 恢复一个已经删除的文件
  - `git checkout <deleting_commit>^ -- <file_path>`

## 8.2`GIT CLEAN`

- `git clean`命令会删除**工作区域的未跟踪文件(untracked files)**
- 使用`--dry-run`标志可以查看什么文件将会被删除
  - 使用`-f`标志将会执行删除操作

- 使用`-d`标志会清除目录

**注意:**该操作不能取消!

![](images/git_clean.png)

## 8.3GIT RESET

- `reset`是另外一命令可以帮助我们来修复错误,传递不同参数将会执行不同功能.
  - 传递路径(with a path)
  - 不传递路径(without a path)
    - 默认地,Git会执行`git reset --mixed`操作

- 对于commits:
  - `git reset`会移动HEAD指针,有选择地修改文件(optionally modifies files)

- 对于文件路径:
  - 不会移动HEAD指针,只会修改文件

### RESET --SORT:移动HEAD指针

执行`git reset --soft HEAD~`命令之前,**工作区域,暂存区域和仓库的状态**如下所示:

![](images/git_reset_soft_before.png)

执行该命令之后,三个区域的状态如下所示,可以发现`git reset --soft HEAD~`的作用仅仅只是**移动HEAD指针**.

![](images/git_reset_soft_after.png)

### RESET --MIXED:移动HEAD指针,拷贝文件到暂存区域

执行`git reset HEAD~`或者`git reset --mixed HEAD~`命令之前,**工作区域,暂存区域和仓库**的状态如下:

![](images/git_reset_mixed_before.png)

执行上面的命令后,三个区域的状态如下图所示,`git reset --mixed HEAD~`**会移动HEAD指针并且将暂存区域的内容替换为HEAD指针指向的commit快照.**

![](images/git_reset_mixed_after.png)

### RESET --HARD:移动HEAD指针,拷贝文件到暂存和工作区域

执行`git reset --hard HEAD~`后,**工作区域,暂存区域和仓库的状态**如下:

将HEAD将要指向的commit快照拷贝到**暂存区域**中

![](images/git_reset_hard_1.png)

然后,根据**暂存区域的commit快照重新生成工作区域中的文件**.

![](images/git_reset_hard_2.png)

### `GIT RESET <COMMIT>`总结

![](images/git_reset_cheat.png)

### `GIT RESET -- <FILE>`

`git reset -- <file>`命令会**将当前HEAD指针指向的commit中的指定文件快照拷贝到暂存区域中**.

执行`git reset -- <file>`命令前**工作区域,暂存区域和仓库**的状态如下图所示:

![](images/git_reset_file_before.png)

执行该命令后,更新后的状态如下图所示:

![](images/git_reset_file_after.png)

### `GIT RESET <COMMIT> -- <FILE>`

`git reset <commit> -- <file>`命令**会将指定commit的指定文件快照拷贝到暂存区域中**.

执行`git reset <commit> -- <file>`命令前**暂存区域,工作区域和仓库的状态**如下所示:

![](images/git_reset_commit_file_before.png)

执行命令后,暂存区域,工作区域和仓库的状态如下所示:

![](images/git_reset_commit_file_after.png)

### `GIT RESET <COMMIT> -- <FILE>总结`

![](images/git_reset_commit_summary.png)

### 使用ORIG_HEAD取消GIT RESET

如果不小心意外地使用了`git reset`命令,我们可以通过GIT保存的**ORIG_HEAD指针(ORIG_HEAD指针保存了前一个HEAD指针的值)**来恢复HEAD指针的指向.

恢复HEAD指针的命令如下:

- `git reset ORIG_HEAD`

## 8.4GIT REVERT - 安全的reset操作

`git revert`命令**会根据指定commit创建一个该commit相反变化(opposite changes)的commit**.该指定的commit还会存在于仓库中.

**提示:**

- 如果你需要从分享的GIT项目中取消一个commit,推荐使用**REVERT**

- REVERT**不会改变commit提交历史**

`git revert <commit>`例子:

查看当前分支的历史:

![](images/git_revert_before.png)

使用`git revert 2b0b3f2`根据该commit创建一个相反状态的commit(**即新创建的commit将不会拥有sha1值为2b0b2f2的commit的changes**)

![](images/git_revert_undo.png)

