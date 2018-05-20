# git使用

## git

git --version

https://github.com/labula8

账号：labula8@qq.com

克隆代码：
    git clone https://github.com/labula8/test.git

同步代码：

    生成秘钥

    > ssh-keygen -t rsa -C "labula8@qq.com"
    > cd .ssh
    > ll
    total 8
    -rw-------. 1 labula8 labula8 1679 Dec 30 03:41 id_rsa
    -rw-r--r--. 1 labula8 labula8  396 Dec 30 03:41 id_rsa.pub

    https://github.com/settings/keys

        Personal settings
            SSH and GPG keys
                labula8-key
                
    > ssh -T git@github.com

    > github 网站创建 cppTest 项目
        git clone https://github.com/labula8/cppTest.git
        
    …or create a new repository on the command line
        echo "# cppTest" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin https://github.com/labula8/cppTest.git
        git push -u origin master

    …or push an existing repository from the command line

    git remote add origin https://github.com/labula8/cppTest.git
    git push -u origin master

    …or import code from another repository

    You can initialize this repository with code from a Subversion, Mercurial, or TFS project.

## 免密码提交代码

    git remote -v

    git remote set-url origin git@github.com:labula8/cppTest.git

    git remote -v
    origin	git@github.com:labula8/cppTest.git (fetch)
    origin	git@github.com:labula8/cppTest.git (push)

> 代码操作

## 更新

    git clone https://github.com/labula8/cppTest.git

    git pull

## 提交

    git add .
    git add a.txt
    git add -A
    git commit -m " commit test"

## 删除

    git rm a.txt

## 状态

    git status
    git remote -v

## 配置
    git init
    git push --set-upstream origin master
    git push -u origin master
    git pull --rebase origin master

    git remote add origin https://github.com/labula8/cppTest.git
    git remote set-url origin git@github.com:labula8/cppTest.git
    git config --global push.default simple

    ssh -T git@github.com












