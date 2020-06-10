# 6-Merging

## 6.1Merge

### 什么是Merge？

从底层来讲，merge commit仅仅就是一个commit。如下图所示：

![](images/merge_commit.png)

### Merge的类型

merge有**两种类型**：

- FAST FORWARD
- NOT FAST FORWARD

#### FAST FORWARD

Fast-forward发生在分支合并时基础分支后只有一个feature分支指向基础分支时。通过`git merge feature`默认会进行Fast-forward合并，如果基础分支后只有一个feature派生，**那么master分支指针会移动到feature分支的最新一个commit上。**

![](images/fast-forward.png)

### NO FAST FORWARD

为了获取合并commit的历史，即使基础分支上没有任何变化，我们还可以通过**not-fast-forward**的方式合并commit，代码如下：

```
git merge --no-ff
```

使用上面的命令会产生一个merge commit，即使创建这个merge commit是没必要的。如下图所示：

![](images/no-ff.png)

## 合并冲突（MERGE CONFLICTS）

当尝试将分支进行合并，文件出现分歧时，Git会停止合并直到冲突解决为止。

![](images/merge_conflict.png)

### GIT RERERE - REUSE RECORD RESOLUTION

git会保存你解决冲突的解决方案，在下一次出现冲突时会复用相同的解决方法。这对于以下两种情况特别有用：

- 长时间存在的特征分支（例如重构）
- rebasing

可以通过以下命令开始它，添加--global标志将会应用到全部项目

```
git config rerere.enabled true
```

![](images/git_rerere.png)

在取消合并后，再次尝试合并，发现git自动应用了之前解决冲突的方法。

![](images/auto_fix_conflict.png)