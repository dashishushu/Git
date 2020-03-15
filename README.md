- # Git

## 下载Git

git官网下载：[下载地址](https://git-scm.com/downloads)

## 打开Git Bash

开始菜单-Git Bash

## 设置名字和邮箱

- 设置全局名字：`git config --global user.name "你的名字"`

- 设置全局邮箱：`git config --global user.email "你的邮箱"`

- 查看已经设置好的全局名字：`git config user.name`

- 查看已经设置好的全局邮箱：`git config user.email`

## 创建版本库

> 对于需要创建一个新的库，来提交新项目

### 在需要的文件夹内创建一个文件夹作为版本库

（例如：我要在`D:\github\dashishushu`内，建立一个名为`god`的版本库）

```shell
cd /d/github/dashishushu && mkdir god && cd god && git init
```

则结果为：

`Initialized empty Git repository in D:/github/dashishushu/god/.git/`
结果为：`初始化空的git版本库成功！`
且在`D:/github/dashishushu/god/`下，有一个`.git`的隐藏文件夹，使用

```shell
ls -a
```

可以看到

```shell
./  ../  .git/
```

### 添加开发完成的代码文件

> (例如`index.js`)到版本库`god`中

- 进入该版本库文件夹内：

  ```shell
  cd /d/github/dashishushu/god
  ```

- 在该目录下，创建一个`index.js`文件

  ```shell
  vi index.js
  ```

- `index.js`的内容如下：

  ```javascript
  let a = 10;
  let b = 11;
  ```

- 保存`index.js`内容后，执行以下命令（添加该文件到git库，以备提交）：

  ```shell
  git add index.js
  ```

- 正式提交该文件到git库（强烈建议提交时，附带上`-m`命令参数，便于阅读提交信息）

  ```shell
  git commit -m "新增一个js文件"
  ```

## 操作版本库内文件

### 修改文件

#### 将index.js文件修改

```js
let a = 100;
let b = 110;
```

#### 使用`git status`命令，查看git当前的状态

```shell
git status
```

结果为：

```shell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.js

```

意思为：文件改变后，还没有到达提交的阶段（得使用`git add index.js`后，方才可以`git commit -m "注释信息"`）。

#### 在`git add index.js`之前，我们通常使用`git diff`来查看，这阶段的改动是否为预期改动：

```shell
git diff
```

结果为：

```shell
$ git diff
warning: LF will be replaced by CRLF in index.js.
The file will have its original line endings in your working directory
diff --git a/index.js b/index.js
index aa8007d..872e8a4 100644
--- a/index.js
+++ b/index.js
@@ -1,2 +1,2 @@
-let a = 10;
-let b = 11;
+let a = 100;
+let b = 110;
```

#### 结果可以看到差异，确认无误后添加到库：

```shell
git add index.js
```

#### 然后提交到库：

```shell
git commit -m "改变a、b两个变量的值"
```

#### 最后，简单查看下git的状态：

```shell
git status
```

结果为：

```shell
$ git status
On branch master
nothing to commit, working tree clean
```

### 版本操作

#### 再次修改`index.js`文件

```shell
vi index.js
```

##### 修改为

```js
let a = 1000;
let b = 1100;
```

##### 再次添加到库、提交到库

```shell
git add index.js
git commit -m "增大a、b两个变量的值"
```

#### 查看git库版本的历史

```shell
git log
```

结果为：

```shell
$ git log
commit 2d3a81127b11b1dd5125bdd1186187707123ff4a (HEAD -> master)
Author: dashishushu <webrim@163.com>
Date:   Mon Mar 9 18:20:16 2020 +0800

    增大a、b两个变量的值

commit 673866b5004e088ccc05e6336b5e85792e211662
Author: dashishushu <webrim@163.com>
Date:   Mon Mar 9 17:48:48 2020 +0800

    改变a、b两个变量的值

commit fcbba2274dab7a13a329d6e16edf9bb589948bc5
Author: dashishushu <webrim@163.com>
Date:   Mon Mar 9 17:27:04 2020 +0800

    新增一个js文件
```

上述结果为，`index.js`文件的版本更改历史

#### 