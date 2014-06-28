title: "使用NVM管理node"

date: 2014-06-28 19:52:41

tags: [node,nvm]
categories:
 node
---
Ubuntu通过`sudo apt-get install node npm`获得的node与npm版本不符，导致**express**，**hexo**，**mongoose**等包安装之后命令无法使用。（所以这个博客是在Win7下用hexo建立的）。  
  今天在Stack Overflow上看到了解决方案，就是通过[nvm](https://github.com/creationix/nvm/)来管理。  
##安装NVM  

* 安装git:  
`sudo apt-get install git git-core`
* clone nvm到 ~/.nvm:  
`git clone https://github.com/creationix/nvm.git ~/.nvm`
* 导入nvm环境: 
`source ~/.nvm/nvm.sh  &&    
[[ -r $NVM_DIR/bash_completion ]] && . $NVM_DIR/bash_completion`
 
在`~/.bashrc`或者`~/.profile`中添加最后一行可以免去每次手动导入nvm环境的麻烦。  

##使用NVM管理Node版本
* 安装指定版本的node:  
`nvm install 0.10.29`或者`nvm install 0.6`  
* 使用某个版本的node:
`vm use node  0.10.29`  
* 查看所有安装版本:
`nvm ls`  
* 回到原环境:  
`nvm deactivate`
* 设置默认版本:  
`nvm alias default 0.10.29`
* 卸载某个版本的node：  
`nvm uninstall 0.10.29`

最后吐槽一下这几个礼拜学习node的感想就是  
* **大二大三**的学弟学妹好强
* 我这样下去会不会失业…………