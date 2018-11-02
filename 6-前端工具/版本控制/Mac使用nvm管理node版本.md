#### 概述

日常工作中，由于node版本更新很快，时常会出现一些依赖在老版本的node下无法运行的问题，这就使得node的版本管理成为一个越来越迫切的需求。

目前常用的node版本管理工具有n和nvm，本文中主要记录nvm的相关内容。

#### nvm安装

`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash`

或者：

`wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash`

安装完成后，可使用`command -v nvm`命令验证是否安装成功。

#### 常用命令

- 安装当前最新稳定版node：

  `nvm install stable`

- 安装指定版本node

  `nvm install <版本号>`

- 显示所有已安装版本

  `nvm ls`

- 切换node版本

  `nvm use <版本号>`

#### 文档参考

https://github.com/creationix/nvm