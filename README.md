# devstack的安装和配置

##0.说明
* > 1.安装配置过程对于使用哪个用户有着严格要求，除非普通用户遇到权限问题，请勿擅自使用`sudo -s`直接切换成root用户，本文中用不到root用户进行配置

* > 2.本教程为devstack解决难问题的小白专门编写，高手勿扰，小白也不要把以往的经验放到这里

* > 3.有任何问题可以微博[@天才小狸猫](http://weibo.com/1736699471)
* >  作为一个iOS开发者和入门云计算开发者，欢迎共同交流学习。


##1.打开Terminal
* 按键盘 control + alt + T 打开终端

##2.检查git安装状态
* 终端中输入`git`

![屏幕快照 2015-12-25 下午1.22.14](media/14510202493251/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202015-12-25%20%E4%B8%8B%E5%8D%881.22.14.png)￼

出现以上界面证明git已安装

> Error：若提示command not found 则继续在终端输入`sudo apt-get install git`
耐心等待安装完成

##3.下载devstack
1.在终端输入 `cd` 回到本用户初始的路径（**极其重要，要不后面教程的路径都要自行修改**）

2.接着在终端输入`git clone git://github.com/openstack-dev/devstack.git`耐心等待git结束并成功

##4.配置stack账户
1.终端cd到git下载下来的devstack/tools
`cd /home/$YOUR_USER_NAME/devstack/tools`
$YOUR_USER_NAME改成当前的用户名

2.创建stack账户
`sudo ./create-stack-user.sh`

##5.配置文件夹权限
1.终端输入`sudo chown -R stack:stack /home/$YOUR_USER_NAME/devstack`

2.为了一劳永逸偷懒输入`sudo chown 777 /etc`

3.继续`sudo chown 777 /opt`

##6.切换到stack账户
由于第四步中实际上是在我们的系统中创建了一个新的名叫stack的账户，而我们的devstack执行配置操作都是在这个账户中完成的，所以

* 终端中输入`su stack`以切换账户
> 如遇密码问题先执行`sudo -s`切换至root再执行`su stack`

##7.修改以及导入配置文件

1.将我给你的已配置好的local.conf文件双击打开

2.到终端中输入`ifconfig`查询所有的网络地址信息

3.将`local.conf`文件中的`HOST_IP=192.168.202.128`后面的地址修改成ifconfig命令查询到的一般是用来网络连接的地址那个地址，修改完成关闭文件

![](media/14510202493251/14510228099505.jpg)

￼
4.使用cp命令将local.conf文件拷贝到`/home/$YOUR_USER_NAME/devstack`目录下，`$YOUR_USER_NAME`依然替换为你的用户名
>由于不确定你的文件位置，以下代码用作示例，根据实际情况修改
>如有权限问题使用sudo解决cp拷贝权限
>！！！再重申一遍，下面地址仅供参考，需要自己修改！！！
`cp /home/davin/Desktop/local.conf /home/davin/devstack/`

##开始运行配置文件脚本

* 输入`cd /home/$YOUR_USER_NAME/devstack`进入路径

* 输入`./stack.sh`开始漫长的等待吧。基本15到30分钟就可以了

>如果中图配置错误，记得留住error信息等待搜索解决
>可以使用`./unstack.sh`取消配置，然后fix bugs。


