# 3-THREE AREAS WHERE CODE LIVES

## 3.1保存代码的三个区域

Git有三个区域来保存代码：

- **工作区域** （Working Area） 
- **暂存区域**（Staging Area）
- **仓库**（Repo）

![](images/where_code_live.png)

### 工作区域

存在于**工作区域**但不存在于**暂存区域的文件**是不会被Git管理的。这些文件也被叫做**未跟踪文件（untracked files）**。

### 暂存区域

**暂存区域**包含了什么是下一次要提交（commit）的文件，它是Git获取**当前提交（commit）**和**下一次提交（commit）**差异的地方。

### 仓库

Git管理的文件都包含在仓库中，包含了你**所有的commits**。

## 3.2更近一步了解暂存区域

### 暂存区域

**注意：**一个干净（**clean**）的暂存区域并不是**空的**。

我们可以把**基准的暂存区域**当做是**最新一次提交（commit）的拷贝**。通过`git ls-files -s`命令我们可以查看暂存区域的内容。

![](images/staging_con.png)

### 移入移出暂存区域的文件

我们可以通过以下命令向暂存区域的添加文件、移出文件或重命名文件：

- 添加一个文件到下一个commit
  - **git add <file>**
- 从下一个commit中删除一个文件
  - **git rm <file>**

- 在下一个commit中重命名一个文件
  - **git mv <file>**

除了上述三个命令外，Git还提供了我们与Git互动地暂存Commits的方式，它允许我们以**块的方式**进行暂存。该命令为`git add -p`。

![](images/in_add.png)

### 从暂存区域中取消暂存文件

从暂存区域移出一个文件不会将该文件彻底移除掉，你只是将**仓库中该文件的一个拷贝替换了暂存区域中的文件。**

![](images/unstage_file.png)

### Git中的内容是怎么移动的？

![](images/how_con_move.png)