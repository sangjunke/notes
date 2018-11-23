## git基本命令
* git clone 网址
* git branch [分支名] 创建分支
* git branch 查看本地所有分支
* git checkout [分支名称] 切换分支
### 写代码
* git status （查看文件改变记录）
* git diff (查看代码级改变)
* git add (1：确认改变)
* git commit -m 提交注释 (2：提交到当前分支的本地工作区)
* git push [远程分支：origin] [本地分支的名称]
* 去git 管理网站创建Merge Request
### 等待合并----管理员合并所有人的Merge Request----
* checkout master (切换至Master)
* git pull (从远程master 更新至 本地master)
* checkout [branch] (切换至本地分支)
* git rebase master [从本地 master 更新当前分支]
* ----是否有冲突----
* ----有----
### ----如何解决冲突----
* 1、在VS中操作代码文件并解决冲突
* 2、git add . 加入待提交
* 3、git rebase --continue 
### ----如果仍然有冲突，重复1/2/3步骤
* 4、git rebase --skip
* 5、git push -f origin [branch] 强推
### -----去网站重新创建Merge Request-------
### 结束，等待合并，重复上述对应步骤.......