---
layout:     post
title:      Git的使用
subtitle:   记录git的一些常用命令
date:       2018-12-4
author:     沈和平
header-img: img/headerImage2.jpeg
catalog: true
tags:
    - Git
---

> 好记性不如烂笔头

### Git一般使用步骤

**1.初始化**  

 `git init`

**2.添加远程库**  

  * 第一种方法：直接Clone with HTTPS链接到本地
  		`git clone https://github.com/shpyoucan/shpyoucan.github.io.git`
  
  * 第二种方法：
  	* 先判断本地仓库是否已经有关联的远程仓库。  
  		`git remote -v`  
  
 	* 添加远程库  
  		`git remote add origin https://github.com/shpyoucan/shpyoucan.github.io.git`   
  
 	* 移除远程库  
  		`git remote remove origin` 
  		
  	* origin 是GitHub默认的远程库名字，可以自定义更改	
  
**3.添加忽略文件**
 
  * 在git工作区根目录下创建`.gitignore`文件，这是一个隐藏文件，可以快捷键`Shift + Command + .`开启显示所有隐藏文件  
  创建.gitignore命令： `touch .gitignore`  
  
  * .gitignore的各种配置，可以查看GitHub，你只需要去组合你所需要的就好。GitHub配置文件清单 [传送门](https://github.com/github/gitignore)
  
  * .gitignore规则不生效
  
   * 原因：.gitignore只能忽略那些没有被git管理跟踪的文件，如果文件已经被git管理了，那么就算你把文件加入.gitignore中也不会忽略的 
   
  	* 解决方案：
  	 * 将缓存区管理的所有文件清除： `git rm -r --cached .` 
  	 * 将工作区文件重新add到缓存区，此时就会按照.gitignore规则add： `git add .`
  	 * 更新本地库git管理的文件： `git commit -m 'update .gitignore'`
  	 * 更新远程库git管理的文件： `git push` 
   
   
**4.添加文件到远程仓库**  

  * 首先添加新增或修改的文件到缓存缓存区：`git add .`  
  * 将缓存区的文件提交到本地仓库并记录描述：`git commit -m "记录描述"`
  * 更新远程库：`git push`
  * 如果提示无法push，提示先 `git pull` 拉取远程库代码，解决方案操作如下：
   * `git fetch origin master:newBranch` origin是远程库名，master是远程库中push向分支的名字，newBranch是新建分支的名字
   * `git branch` 查看当前分支，* 所在表示的是当前分支
   * `git merge newBranch` 将master分支和newBranch合并
     1. 出现 *Merge branch 'branchName'*，是提示合并时，需要输入合并记录，执行 `i` 进入可编辑，编辑完按键盘 `Esc` 键退出编辑状态，之后执行 `:wq` (退出不了就执行 `:wq!` ) 退出信息记录界面。此时，再执行 `git push` 将本地库更新到远程库即可。
     2. 如果没有出1的情况，出现 *Merge conflict in xxxx* , 这是提示有冲突，用 `git status` 查看哪些文件有冲突（both modified：xxxx ），解决完冲突，执行 `git add .` ，再执行 `git commit -m "冲突记录"` 更新本地库，最后执行 `git push` 将本地库更新到远程库



