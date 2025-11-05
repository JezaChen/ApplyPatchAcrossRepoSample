# 跨仓库应用Git提交的方法 - 示例代码

文档链接: https://jeza.net/2025/11/05/Git-Apply-Patch-Across-Repos/

## 过程

首先clone本仓库：

```shell
git clone --recursive https://github.com/JezaChen/ApplyPatchAcrossRepoSample 
cd ApplyPatchAcrossRepoSample
```

进入repoA子仓库，对dev分支最近的两次提交输出一个补丁文件：

```shell
cd repoA
git checkout dev
git format-patch -2 dev --stdout > my.patch
```

移动补丁文件到repoB子仓库中，并进入repoB，应用补丁：

```shell
mv my.patch ..\repoB
cd ..\repoB
git apply my.patch -p2 --directory="Source"
```

此时使用`git status`查看repoB的状态，可以发现补丁被应用上了。

