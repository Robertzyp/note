# Git 版本控制工具
  1. 配置登陆用户名邮箱
  ```git
  git config --global user.name "YOUR NAME"
  git config --global user.email "YOUR EMAIL ADDRESS"
  ```
  2. 生成密钥
  
    `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
  3. 本地初始化
  
    `git init`
  4. 添加到暂存区
   
    `git add`
  5. 提交到本地分支
   
    `git commit -m // 必须添加解释`
  6. 推到远程分支
   
    `git push// 此时必须绑定到远程分支`