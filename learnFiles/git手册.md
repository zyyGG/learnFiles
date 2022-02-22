1. 本地库初始化 
   1. 进入本地文件 cd , mkdir(创建文件夹)
   2. 初始化.git init  
   3. 查看隐藏文件 ls -la
   注意：.git目录中存放的是本地库相关的目录和文件，不要删除和胡乱的修改
2. 设置签名
   1. 形式  
   用户名：xxx
   Email 地址：AAA@qq.com
   2. 作用：区分不同开发人员的身份
   3. 辨析：这里设置的签名和登录远程库(代码托管)的账号，密码没有任何关系
   4. 命令：
      1. 项目级别/仓库级别：仅在本地库范围内有效
         1. git config user.name Tom_pro
         2. git config user.mail GoodMorning_pro@mailbox.com
         3. 信息保存位置: .git/config
      2. 系统用户级别：登录当前操作系统的用户范围
         1. git config --global user.name Tom_pro
         2. git config --global user.mail GoodMorning_pro@mailbox.com
         3. 信息保存的位置：~/.gitconfig
      3. 优先级
         1. 就近原则：项目级别优先于系统用户级别，二者都有时，采用项目级别的签名
         2. 如果只有系统用户级别的签名，当然就以系统用户级别的签名为准
         3. 二者都没有不允许
   5. 其他命令: 查看某个文件 cat .git/config
3. 基本操作
   1. 状态查看操作 
      git status
      查看工作区，暂存区状态
   2. 添加操作 
      git add[file name]
      将工作区的"新建/修改"添加到暂存区
   3. 提交操作 
      git commit -m "commit message"[file name]
      将暂存区的内容提交到本地库
   4. 查看历史记录
      git log 显示最完整的形式
      多屏显示的控制方式
         空格向下翻页
         b向上翻页
         q退出
      git log --pretty=oneline
      简洁的显示方式，在一行内
      git log --oneline
      更简洁的显示方式：在一行内
      git reflog
      在oneline基础上，还显示了HEAD@{移动到当前版本需要多少步}
5. 版本的前进后退
   1. 基于索引值操作[推荐]
      1. git reset --hard [局部索引值]
      2. git reset --hard e2709ad9
   2. 使用^符号
      1. 只能后退版本 
      2. git reset --hard HEAD^
      3. 注意：一个^表示后退一步，n个^表示后退n步
   3. 使用~符号
      1. 只能后退版本
      2. git reset --hard HEAD~n
      3. 注意：n表示后退n步
6. reset 的参数
   1. --soft 参数
      1. 仅仅在本地库移动HEAD指针
   2. --mixed 参数
      1. 在本地库HEAD指针
      2. 重置暂存区
   3. --hard 参数
      1. 在本地库移动HEAD指针
      2. 重置暂存区
      3. 重置工作区
7. 删除文件并找回
   1. 前提：删除前，文件存在时的状态提交到了本地库
   2. 操作：git reset --hard [指针位置]
      1. 指针位置：历史记录或当前位置
         1. 删除操作已经提交到本地库：指针位置指向位置记录
         2. 删除操作尚未提交到本地库：指针位置使用HEAD
8. 比较文件差异
   1. git diff[文件名]
      1. 将工作区中的文件和暂存区进行比较
   2. git diff [本地库中历史版本] [文件名]
      1. 将工作区中的文件和本地库历史记录比较
9. git 的分支
   1. 在版本控制中，使用多条线来开发
   2. 分支的好处
      1. 同时并行推进多个功能的开发，提高开发的效率
      2. 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败额分支删除重新开始即可。
   3. 分支操作
      1. 创建分支
         1. git branch [分支名]
      2. 查看分支
         1. git branch -v
      3. 切换分支
         1. git checkout [分支名]
      4. 合并分支
         1. 切换到接受修改的分支上(被合并，增加新内容)上
            1. git checkout [被合并分支名]
            2. git checkout master
         2. 执行marge命令
            1. git merge [有新内容分支名]
            2. git merge hot_fix
      5. 解决冲突
         1. 编辑文件，删除特殊符号
         2. 把文件修改到满意的程度，保存退出
         3. git add[文件名]
         4. git commit -m "日志信息"
            1. 注意：此时commit 一定不能带有具体的文件名
10. 链接远程库
    1.  创建链接的快捷方式
        1.  git remote -v 查看所有的简称
        2.  git remote add [简称] [地址]
        3.  git push [地址] [HEAD] / git push origin https://github.com/zyyGG/myProject.git
11.  克隆效果
    1.  命令
        1.  git origin [远程地址]
    2.  效果
        1.  完整的把远程库下载到本地
        2.  创建origin远程地址别名
        3.  初始化本地库
12. 拉取
    1.  pull = fetch + merge
    2.  git fetch [远程库地址别名] [远程分支名] git fetch origin master
    3.  git merge [远程库地址别名/远程分支名]
    4.  git pull [远程库地址别名] [远程分支名]

14. 解决冲突
    1.  要点
        1.  如果不是基于GitHub远程库的最新版所做的修改，不能推送，必须先拉取
        2.  拉取下来后入股进入冲突状态，则按照“分支冲突解决” 操作解决即可。  
15. 跨团队协作