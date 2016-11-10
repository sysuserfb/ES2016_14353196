#ROS配置安装日志
>本次安装的是ros的jade版本<br>
>强推链接  [在Ubuntu中安装ROS Jade](http://wiki.ros.org/cn/jade/Installation/Ubuntu)

1. 配置Ubuntu软件仓库(repositories)
你的ubuntu软件仓库必须允许"restricted","universe","multiverse"这三种安装模式，如图:<br>
![repositories](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/2016-11-09-21-56-04.png)
2. 配置sources.list将软件源添加到sources.list 使得电脑能够安装来自packages.ros.org的软件包（注意ROS Jade仅支持Trusty (14.04)、Utopic (14.10) 和 Vivid (15.04)）
  ```
  $ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
  ```
  * 假如镜像下载速度不够快的话可以换源成国内的镜像源

3. 添加keys
  ```
  $ sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
  ```
4. 安装
  * 按照惯例来一个`$ sudo apt-get update`
  * 推荐安装桌面完整版 `$ sudo apt-get install ros-jade-desktop-full`
  5. 安装完毕即可对rosdep进行初始化
  ```
  $ sudo rosdep init
  $ rosdep update
  ```
6. 最后我们为ROS添加环境变量，使得每次打开终端都是自动设置好环境变量

  ```
  $ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
    # 使环境变量设置立即生效
  $ source ~/.bashrc
  ```
  ![path](https://raw.githubusercontent.com/sysuserfb/ES2016_14353196/master/20161110120238.jpg)
7. 最后的最后我们可以安装一个rosinstall工具，通过这个命令可以轻松的下载许多ROS软件包
  ```
  $ sudo apt-get install python-rosinstall
  ```
- ROS配置安装到此结束。
