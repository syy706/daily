# ssh 相关

## 设置全局配置

git config --global user.name '' && git config --global user.email ''

### 查看默认配置

git config user.name
git config user.email

## 查看现有 ssh 密钥

ls -al ~/.ssh

## 生成公钥/私钥

### 生成默认密钥

ssh-keygen -t rsa -C "邮箱"

### 生成特定密钥（文件名自定）

ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "邮箱"

## 配置 config

cd ~/.ssh
touch config

添加内容

Host \*github.com
IdentityFile ~/.ssh/id_rsa.github
User "userName"

## 上传 ssh key

登陆 github 或 gitlab

setting => Add SSH Key, 添加默认/特定密钥

## 测试 gitlab

ssh -T git@github.com

## 测试 github

ssh -T git@gitlab.com

有时候 ssh 会报错

遇到如下异常：

connect to host git.midea.com port 22: Connection timed out

fatal: Could not read from remote repository.

原因是代理软件将 22 端口占用，改为 443

config 文件修改配置为:
Host github.com
HostName ssh.github.com
Port 443
User username

## 其他

git init / git clone 时，默认使用 git 全局配置，推送代码时会出现头像/名称异常，可以在项目内容手动设置用户名/密码

git config user.name "" && git config user.email ""
