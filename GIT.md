- [初始化本地仓库](#%e5%88%9d%e5%a7%8b%e5%8c%96%e6%9c%ac%e5%9c%b0%e4%bb%93%e5%ba%93)
  - [状态查看](#%e7%8a%b6%e6%80%81%e6%9f%a5%e7%9c%8b)
  - [添加操作](#%e6%b7%bb%e5%8a%a0%e6%93%8d%e4%bd%9c)
  - [删除操作](#%e5%88%a0%e9%99%a4%e6%93%8d%e4%bd%9c)
  - [提交操作](#%e6%8f%90%e4%ba%a4%e6%93%8d%e4%bd%9c)
- [版本前进和后退](#%e7%89%88%e6%9c%ac%e5%89%8d%e8%bf%9b%e5%92%8c%e5%90%8e%e9%80%80)
  - [日志查看](#%e6%97%a5%e5%bf%97%e6%9f%a5%e7%9c%8b)
  - [后退向前](#%e5%90%8e%e9%80%80%e5%90%91%e5%89%8d)
  - [reset 命令的三个参数对比](#reset-%e5%91%bd%e4%bb%a4%e7%9a%84%e4%b8%89%e4%b8%aa%e5%8f%82%e6%95%b0%e5%af%b9%e6%af%94)
- [比较文件](#%e6%af%94%e8%be%83%e6%96%87%e4%bb%b6)
- [GIT分支](#git%e5%88%86%e6%94%af)
  - [什么叫分支](#%e4%bb%80%e4%b9%88%e5%8f%ab%e5%88%86%e6%94%af)
  - [分支的好处](#%e5%88%86%e6%94%af%e7%9a%84%e5%a5%bd%e5%a4%84)
  - [操作分支](#%e6%93%8d%e4%bd%9c%e5%88%86%e6%94%af)
    - [查看分支](#%e6%9f%a5%e7%9c%8b%e5%88%86%e6%94%af)
    - [创建分支](#%e5%88%9b%e5%bb%ba%e5%88%86%e6%94%af)
    - [切换分支](#%e5%88%87%e6%8d%a2%e5%88%86%e6%94%af)
    - [合并分支](#%e5%90%88%e5%b9%b6%e5%88%86%e6%94%af)
    - [解决冲突](#%e8%a7%a3%e5%86%b3%e5%86%b2%e7%aa%81)
- [GIT文件管理机制](#git%e6%96%87%e4%bb%b6%e7%ae%a1%e7%90%86%e6%9c%ba%e5%88%b6)
  - [推送](#%e6%8e%a8%e9%80%81)

## 初始化本地仓库
    git init
    .git 隐藏的 存放的是本地库相关的目录和文件,不能随便删除修改
>
    设置签名
    user:
    Email:
    作用:区分不同开发人员的身份
    设置的签名和远程登陆库的账号密码没有任何关系
>
    命令
    项目级别/仓库级别: 尽在本地库范围生效
>git config user.name Kita_Shizuku

>git config user.email kitayama@shizuku.com
        
>保存位置 /.git/config

        
    系统用户级别:登陆当前操作系统的用户范围
>git config --global user.name Kitayama_Shizuku

>git config --global user.email
        kitayama_glb@shizuku.com

>保存位置
        ~/.gitconfig

    二者都没有不允许

### 状态查看
>git status

    on branch mastar 主干
    No commits yet 没有提交
    nothing to commit 没有可以提交的

### 添加操作
>git add [file name]

### 删除操作
>git rm --cached good.txt
    
    从暂存区中移除整个文件

### 提交操作
>git commit good.txt

    提交到本地库

>git commit -m "message" [filename]

git add -> 暂存区 -> git commit -> 本地库

## 版本前进和后退
### 日志查看
>git log

    commit a2fcb8b941cf77d43ac88987cf1380fa30d89655 (HEAD -> master)
    Author: Kitayama_SHIZUKU <kitayama@shizuku.com>
    Date:   Wed Mar 25 14:23:39 2020 +0800

head相当于指针 , 做前进后退版本操作就是移动head的指针
    
    多屏显示控制方式
        空格向下翻页
        b向上翻页
        q退出

>git log --pretty=oneline

>git log --online

一行显示日志

>git reflog
    
    8901a09 (HEAD -> master) HEAD@{0}: commit: SECOND COMMIT CATALINA
    6fa79ef HEAD@{1}: commit: CATALINA TXT
    a2fcb8b HEAD@{2}: commit: second vim better
    8b663c0 HEAD@{3}: commit (initial): my first commit

HEAD@{num} 表示要回退某一版本的步数

### 后退向前
- 基于索引值操作[推荐]
- 使用^符号
- 使用~符号
  
>git reset --hard [索引值]

    HEAD is now at 6fa79ef CATALINA TXT

现在指针指向 6fa79ef 这个版本了

>git reflog

    6fa79ef (HEAD -> master) HEAD@{0}: reset: moving to 6fa79ef
    8901a09 HEAD@{1}: commit: SECOND COMMIT CATALINA
    6fa79ef (HEAD -> master) HEAD@{2}: commit: CATALINA TXT
    a2fcb8b HEAD@{3}: commit: second vim better
    8b663c0 HEAD@{4}: commit (initial): my first commit

>git reset --hard HEAD^ //一个^后退一步

>git reset --hard HEAD~3 //后退三步

### reset 命令的三个参数对比
>--soft

    仅仅在本地库移动指针
    本地库和暂存区不一致, 暂存区和工作区一致为绿色
>--mixed

    在本地库移动HEAD指针, 重置暂存区 
    工作区和本地库暂存区不一致, 显示为红色

>--hard

    移动HEAD指针, 重置暂存区和工作区

## 比较文件
>git diff CATALINA.txt

将工作区的文件和暂存区进行比较

    diff --git a/CATALINA.txt b/CATALINA.txt
    index 70b680d..3dfda0a 100644
    --- a/CATALINA.txt
    +++ b/CATALINA.txt
    @@ -2,4 +2,5 @@ mojave
    catalina
    KITAYAMA_SHIZUKU
    ASHIYA_IZUMI
    +------
    AYA

>git diff [本地库历史版本][文件名]

将工作区中的文件和本地库历史记录比较

>git diff HEAD 

比较当前工作区所有的文件

## GIT分支
### 什么叫分支
版本控制过程中, 使用多条线同时推进多个任务
- master
- feature_blue
- feature_game
- hot_fix

### 分支的好处
- 同时推进多个功能开发
- 如果一个分支开发失败,不会对其他分支又任何影响

### 操作分支
#### 查看分支
>git branch -v

    * master b386fb4 WHERE IS MY CODES JS

#### 创建分支
>git branch hot_fix

     hot_fix b386fb4 WHERE IS MY CODES JS
    * master  b386fb4 WHERE IS MY CODES JS

#### 切换分支
>git checkout hot_fix

    Switched to branch 'hot_fix'

修改了hot_fix分支的内容

    * hot_fix 26e4d01 UPDATA BY HOT_FIX
    master  b386fb4 WHERE IS MY CODES JS

#### 合并分支
1. 切换到接受修改的分支
2. 执行merge命令
>git merge hot_fix

    Updating b386fb4..26e4d01
    Fast-forward
    CATALINA.txt | 2 ++
    1 file changed, 2 insertions(+)

#### 解决冲突
1. 编辑文件, 产出特殊符号
2. 把文件修改到满意程度, 保存退出
3. git add[文件名]
4. git commit -m "日志信息"
    - 此时commit不能带有文件名

```
    Auto-merging CATALINA.txt
    CONFLICT (content): Merge conflict in CATALINA.txt
    Automatic merge failed; fix conflicts and then commit the result.
```
    <<<<<<< HEAD (Current Change)
    __UPDATE BY HOT_FIX
    =======
    __UPDATE BY MASTER 
    >>>>>>> master (Incoming Change)

>git status

    On branch hot_fix
    You have unmerged paths.
    (fix conflicts and run "git commit")
    (use "git merge --abort" to abort the merge)

    Unmerged paths:
    (use "git add <file>..." to mark resolution)

            both modified:   CATALINA.txt
> git add CATALINA.txt

    On branch hot_fix
    All conflicts fixed but you are still merging.
    (use "git commit" to conclude merge)

    Changes to be committed:

        modified:   CATALINA.txt

>git commit -m "resolve confilict"

不带文件名, 提交文件解决合并冲突

    [hot_fix 7ac67ff] resolve confilict

## GIT文件管理机制
 Git把数据看作是小型文件系统的一组快照.
 每次提交更新时Git都会对当前的全部文件 制作一个快照保存这个快照的索引. 为了高效如果文件没有修改, Git不在重新存储该 文件, 而是只保留一个链接指向之前存储的 文件, 所以Git的工作方式可以成为快照流.

 每个快照保存parent的hush

 ##GITHUB
>git remote -v

>git remote add [别名] [地址]

    tig     https://github.com/ZunbaRan/TIG_BUHTIG.git (fetch)
    tig     https://github.com/ZunbaRan/TIG_BUHTIG.git (push)

fetch地址用来取回
push地址用来推送

### 推送
>git config --global credential.helper store

第一次登陆输入用户名密码 , 记住用户名密码下次不用输入

>git pull origin master --allow-unrelated-histories 

把远程仓库和本地同步，消除差异
>git push [别名][分支]




