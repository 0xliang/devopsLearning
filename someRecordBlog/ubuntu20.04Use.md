# some record for use ubuntu20.04

### use VNC

使用vnc连接远程ubuntu系统时，出现了几个问题：
  * 安装好tigervnc后，远程连接出现黑屏，目前解决方法是：安装一个xfce桌面，本地登录时使用xfce，此时远程连接就可以有画面了

安装步骤：
1. `sudo apt install tigervnc`
2. `vncpasswd`
3. 创建xstarup文件，内容如下
    ```
    liangros3@liangros3:~$ cat .vnc/xstarup 
    #!/bin/sh                                                                       
    unset SESSION_MANAGER
    unset DBUS_SESSION_BUS_ADDRESS
    export XKL_XMODMAP_DISABLE=1
    export XDG_CURRENT_DESKTOP="GNOME-Flashback:GNOME"
    export XDG_MENU_PREFIX="gnome-flashback-"
    [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
    [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
    xsetroot -solid grey    #设置背景色
    vncconfig -iconic &    #
    #gnome-terminal &    #连接后会直接打开一个terminal窗口
    #nautilus &    #连接后会直接打开一个文件窗口
    gnome-session --session=gnome-flashback-metacity --disable-acceleration-check & 
    ```

远程桌面可以使用vncviewer连接：本次使用[realvnc](https://www.realvnc.com/en/connect/download/viewer/)的客户端
