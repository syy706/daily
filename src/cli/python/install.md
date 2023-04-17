通过 pyenv 来管理 python 版本，但是 pyenv 只能管理通过 pyenv 来安装的 python

## 安装 pyenv

brew update
brew install pyenv

## 查看可安装的 python 脚本

pyenv install -l

## 安装指定版本

pyenv install 3.8.12

## 查看已安装的 python 版本

pyenv versions

## 设置全局和当前版本

pyenv global 3.9.2
pyenv local x.x.x
