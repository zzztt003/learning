# Git
**一种分布式版本控制系统**
使用仓库存储每个文件的版本变化，可恢复 
svn、是集中式的版本控制系统 
分布式的是所有本地都有完整的版本库 

典型工作流程： 
![image.png](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721720046234-9598063b-4969-4078-873b-89d2c186c8ae.png#averageHue=%23828282&clientId=uefd47a24-4a55-4&from=paste&height=546&id=u7f9b8031&originHeight=1365&originWidth=858&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=140619&status=done&style=none&taskId=u735a237e-6e45-49d7-8587-f01154de809&title=&width=343)
![image.png](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721720066219-7098d618-42ac-4f73-b7fd-6fe492ebbbe7.png#averageHue=%239f9f9f&clientId=uefd47a24-4a55-4&from=paste&height=164&id=u5e87beb7&originHeight=409&originWidth=898&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=44706&status=done&style=none&taskId=u5a0187da-022e-4c98-90d6-0b6f517a3be&title=&width=359.2)


# 基础
### 安装和配置
cmd git -v 查看版本 
windows可以使用git bash 

![配置用户名和邮箱，查看配置信息 ](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721720889498-56250e37-2ceb-48df-b18d-52631a441f04.png#averageHue=%230b0a08&clientId=uefd47a24-4a55-4&from=paste&height=152&id=u7514480a&originHeight=381&originWidth=767&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=46433&status=done&style=none&taskId=u418fec8a-0f57-4ede-b54f-5528b6a3b9b&title=&width=306.8) 
版本库，又叫仓库，repository，简称repo

### 简单命令
```bash
初始化仓库：
git init
克隆仓库：
git clone
```

```markdown
mkdir dirname ——创建新目录
cd dirname ——进入
ls ——枚举所有目录（不包括隐藏）
ls -a ——包括隐藏 -ltr
cd .. ——退回上级目录
```

```bash
查看仓库状态：
git status
```

```markdown
echo "this is the first file" > file1.txt  ——创建文件
cat file ——查看文件
vi file ——修改文件
i ——编辑界面进行内容编辑
esc ——退出内容编辑
:wq ——保存并退出编辑界面
rm file ——删除文件 

git add *.txt ——添加所有以txt结尾的文件
git add .  ——添加当前文件夹下所有文件
```
```bash
将文件加入暂存区：
git add filename
  . 所有文件
```
```bash
将某暂存区文件改为untrack：
git rm --cache filename
```

```bash
将暂存区文件提交到版本库：
git commit （-m "提交信息"）
```
```bash
查看版本库提交历史记录：
git log （--oneline 更简洁）
```

```bash
回退到某个版本：
git reset 参数 版本id
  --soft 本地仓库回退到某一个版本，保留工作区和暂存区的所有修改内容（把提交的放回暂存区？）
  --hard ，丢弃工作区和暂存区的所有内容（删除所有提交？）
  --mixed ，保留工作区，丢弃暂存区的所有内容（把提交的放回工作区？）
  --keep ?

    HEAD^ / HEAD~ 上一个版本？
    HEAD~n n 个版本 ？
```

```bash
列出当前目录所有被git管理的文件（主要是暂存区）：
git ls-files
  -c / --cache 仅显示暂存区中的
  -m / --modified
  -d / --deleted
  -o / -others
  -i / -ignored
```

```bash
查看所有git相关的操作记录：
git reflog
```

```bash
查看xx和yy之间的差异：
只显示xx和yy中内容不同的同名文件之间的差异

git diff 
  无参数 显示工作区和暂存区之间。。。的差异
  HEAD 显示工作区和本地仓库之间
  --cached 显示暂存区和本地仓库之间
  
    filename 只显示某文件的差异

？  版本id1 版本id2 显示本地仓库两个版本之间（2相对1来说增加、减少了什么）
```

```bash
从版本库中删除文件：
git rm 参数 filename
  无参数 把文件从工作区和暂存区都删除
  --cached 从暂存区删除，但工作区保留
```

### 三种区域解释

1. 工作区（本地工作目录） .git所在目录
2. 暂存区（临时存储即将要提交到git的文件） .git/index
3. 本地仓库（完整项目历史）  .git/objects

![image.png](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721721622079-ef0ee2ce-b772-4c17-96b5-d653d0eb3ab6.png#averageHue=%233696b9&clientId=uefd47a24-4a55-4&from=paste&height=226&id=u0ecddd3b&originHeight=566&originWidth=1344&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=251410&status=done&style=none&taskId=u14772f22-a1af-4486-80b4-9e9a5011d51&title=&width=537.6)
工作区的文件添加到暂存区后，工作区文件不在了
暂存区文件提交到本地仓库后，暂存区文件也还在？

### 四种文件状态

1. 未跟踪 untrack
2. 未修改 unmodified
3. 已修改 modified 
4. 已提交 staged

![image.png](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721721784256-8dfe9874-5ab5-4f41-a276-e505cbda039f.png#averageHue=%23a7fbab&clientId=uefd47a24-4a55-4&from=paste&height=295&id=u9279d2d5&originHeight=737&originWidth=1514&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=236532&status=done&style=none&taskId=u9d5d4d3e-5b63-40a7-99b5-bfdf260f4fe&title=&width=605.6)
创建文件->untrack

### .gitignore 文件
有些文件不应该被加入本地仓库，如：
![image.png](https://cdn.nlark.com/yuque/0/2024/png/35664476/1721797489658-02f4d40c-a832-4c25-8353-126a6dd0c181.png#averageHue=%232c7bc2&clientId=ub2da373e-d5aa-4&from=paste&height=223&id=u31dbcd3c&originHeight=557&originWidth=1168&originalType=binary&ratio=2.5&rotation=0&showTitle=false&size=370150&status=done&style=none&taskId=uc69dbde3-9354-41ac-8171-2118c20429a&title=&width=467.2)
可以在.gitignore文件中列举出来，使得git管理控制时忽略它们（生效前提是这些文件没有被添加到版本库中）
```bash
*.log	忽略所有以.log结尾的文件
temp/ 忽略temp文件夹的所有文件

```
### 远程仓库和本地仓库的同步
