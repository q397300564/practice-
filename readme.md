## 自述一下git的简单使用：

   #### 第一步： 先要下载git 和 创建github 的账户

 ### 起步：初次使用需要设置姓名和邮箱
     git config --global user.name "你的姓名"
     git config --global user.email "luodan911221@gmail.com"

 ### clone 项目：用于把github 上的项目　clone(下载)到本地
     git clone git@github.com:q397300564/practice-.git
 * 如果这个时候提示clone 没成功　就说明要设置公私钥
 * 如何设置公私钥：ssh-keygen -t rsa -b 4096 -C "luodan911221@gmail.com"  (这里的邮箱就是github　的邮箱)
 * 一直回车，最后在~/.ssh目录下生产了公钥id_rsa.pub和私钥id_rsa
 * 打开公钥文件id_rsa.pub 复制里面的内容
 * 打开github，点击头像进入和个人设置，找到　ssh 设置添加 ssh key 
      
      
       cd practice- (跳转到文件夹 practice- 中)

 ### 添加文件并提交

  #### 创建文件
    touch a.md
    git status (查看工作区)

  #### 添加文件到暂存区
    git add index.html (这是添加index.html到暂存区　全部的话. 就好了)

  #### 把暂存区的更新提交到本地库
    git commit -am 'add file' (这里时把暂存区的文件添加到本地库'' 单引号里面的是提示做了上面)

  #### 把本地库的的改动推送到远程库origin的master分支 
    git push origin master


 ### 修改删除文件

  #### 把远程仓库的变更合并到本地仓库
    git pull

  #### 修改文件
    vim a.md
    git add .
  * 这里需要注意，如果提交包含大量字符串，提交参数不用加m
  * 此时会进入 vim 界面, 按下 i 切换到insert模式下，进行编辑
  * 编辑完成后按下　ESC 进入normal模式下，　输入　:wq 保存退出　vim

   git commit -am 'add file'
   git push origin master

  #### 删除文件
    rm -rf a.md (包括文件夹也可以删除　如果没有-rf 只能删除文件)
    git add .
    git commit -am '删除a.md'
   如果之前就git push origin master 过，后面可以直接简化成　git push
   
    git push 


## 问题
* git clone url 和　git pull 的区别？
* 本地仓库和远程仓库的区别？
* origin 代表什么？
 
  #### git clone url 和 git pull 的区别
   * 从字面意思也可以理解，都是往下拉代码，git clone 是克隆, git pull 是拉
   * 但是区别：
    * 从远程服务器克隆一个一模一样的版本库到本地，复制版本库，叫做clone (clone是将一个库
　　　复制到你的本地，是一个本地从无到有的过程)
    * 从远程服务器获取一个branch分支更新到本地，并更新本地库，叫做pull (pull是指同步一个
　　　在你本地有版本的库内容更新的部分到你的本地库)

  #### 本地仓库和远程仓库的区别？
   * 本地仓库也是实际在电脑上看到的这个目录，但是要 git commit -am '版本名'缓存区中的更改才
　　　能保存到本地库中。
  
   * 而远程库当然时远程服务器上那个项目的目录啦，就需要 git push origin master 本地库的修改
　　　才能保存到你下载的这个本地库的远程库中！

  #### origin 带表了什么？
  * origin表示远程仓库，是你在clone的时候git自动设置的远程仓库的别名

## 复杂使用

 ### 本地创建一个git项目推送到远程仓库
  #### 创建一个文件夹
       mkdir newProject
  #### 切换到新建的文件夹　newProject 中
   * 把一个文件夹初始化成一个本地git仓库
   * 注意　仓库和文件夹的区别在与仓库下有个隐藏的 .git 文件夹，里面有些信息
   * 对于一个远程仓库，删除 .git 文件夹，就变成了一个普通的文件夹
　　
  #### 初始化文件夹
　    git init
 
  #### 新建文件　index.html
       touch index.html
   
  #### 用 vim 修改文件内容
       vim index.html
   
  #### 添加文件到暂存区 
       git add .
　　
  #### 把暂存区的文件添加到本地仓库
       git commit -am '修改内容的记录'
　　
  #### 查看本地库里记录的远程库地址
       git remote -v

  #### 这里把远程库的地址添加个标签叫origin
       git remote add origin git@github.com:q397300564/practice-.git

  #### 推送到远程库地址
       git push origin master　   

  #### 在添加一个远程库的标签
       git remote add gitlab git@github.com:abc/blog.git

  #### 推送到gitlab标签的地址上
       git push gitlab master

  #### 删除gitlab 标签 
       git remote remove gitlab

  #### 修改origin标签对应的地址
       git remote set-url origin git@github.com:jirengu/blog3.git

  #### 把gitlab 标签改名为 coding 
       git remote rename gitlab coding

 ### 分支操作

  #### 创建本地库box 分支
       git branch box

  #### 切换到box 分支
       git checkout box

       touch b.md
       git add .
       git commit -am 'add  b.md'
  
  #### 推送到origin地址的box 分支上
       git push origin box

 ### 分支合并
  #### 切换到master 分支上
       git checkout master

  #### 把box 分支上的内容合并到当前分支(master)上
　　    git merge box
      
 ### 冲突
   #### 当自己和别改同一个文件的同一个地方的时候，在执行git pull时更新到本地合并时会出现冲突
   * 修改冲突的文件
   * 重新提交

## bug 

 ### 如果出现了这样的报错
      error: 无法推送一些引用到 'git@github.com:q397300564/practice-.git'
      提示：更新被拒绝，因为您当前分支的最新提交落后于其对应的远程分支。
      提示：再次推送前，先与远程变更合并（如 'git pull ...'）。详见
      提示：'git push --help' 中的 'Note about fast-forwards' 小节。
 #### 那么就用
      git push -u origin +master
