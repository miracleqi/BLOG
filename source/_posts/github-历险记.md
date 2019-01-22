title: github 历险记
author: MiracleQi-温柔魔君
tags:
  - git
  - github
categories:
  - Linux
  - Windows
date: 2016-07-01 16:18:00
cover: /img/post-cover/24.jpg
---
最近公司准备将 WAF4 代码开源

这里将学习 github 步骤及进度记录一下（只记录必要过程）

# 环境

1. 创建github账户

2. 客户端安装git

3. 初步设置 git
```
$ git config --global user.name "xxxx"
$ git config --global user.email "yyyy@gmail.com"
```
4. 获取ssh公钥

 ```
cd ~/.ssh
ssh-keygen -t rsa -C “yyyy@gmail.com”
```

 输入要生成密钥文件的名称与密码（也可连续三个回车键）

 此时生成密钥文件和公钥文件（.pub）

 注：若自定义密钥文件名称，而不是敲回车默认

 则需 ```ssh-add ~/.ssh/y_rsa``` （y_rsa为密钥文件名称）

 若 ```ssh-add``` 报错 ```Could not open a connection to your authentication agent```

 则需执行  ```ssh-agent bash```，再执行 ```ssh-add```

 不然 ssh 连接 github 时找不到密钥文件会提示 ```Permission denied (publickey).```

5. GITHUB 添加 SSHKEY

 setting --> SSH and GPG keys --> New SSH keys

6. 客户端测试
 ```
ssh -T ​git@github.com
```
 成功则提示：```Hi  name! You're sucessfully ...```

 若提示 ```Permission denied (publickey).```

 可通过 ```ssh -vT git@github.com``` 查看详细错误信息

 我这边报错显示，没有找到密钥文件，通过上面 4 中的方法得到解决

# 项目

1. 创建新的项目test（远程仓库）

 github 上 Create a new repository

 项目名称为 test

 项目路径为 https://github.com/290557551/test

2. 本地添加 github 远程仓库

 2.1 git clone
  ```
    git clone git@github.com:290557551/test.git
    cd test
    git remote -v
        origin  git@github.com:290557551/test.git​ (fetch)
        origin  git@github.com:290557551/test.git​ (push)
    git branch
        * master
   ```
  2.2 手动添加
  
   若不用git clone，则手动添加
   ```
    mkdir  test
    cd test
    git init
    git remote add origin git@github.com:290557551/test.git
    git push origin master
   ```
    到此已经将本地仓库与远程仓库连接起来，并可以上传或修改代码了​

3. 修改
```
git add  用于添加文件或目录
git status 查看当前状态
git commit -a -m "提交的描述信息"  将变动提交到仓库
git push origin master 将变动提交至 github
```

# 随记

 3.1 github markdown table

        dog | bird | cat

        ----|------|----

        foo | foo  | foo

        bar | bar  | bar

        baz | baz  | baz