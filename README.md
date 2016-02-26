# SS-Regenerater 自动安装包

感谢 http://www.hostloc.com/thread-305480-1-1.html 公开序列号的算法<br>
也感谢ss官方群突如其来的爆料一张lic核心代码<br>

闲着蛋疼做了一个自动安装脚本,仅限Ubuntu14.04和14.10,服务器上保存着几乎所有的该系统内核,如果需要其他内核,麻烦自行寻找<br>
上传了服务端源码,非常简单的几句代码(也是我写过最简单的代码)<br>

### 首次写linux shell 肯定写的不太好 请多指教

servspdInstaller.sh 为一键安装(无需修改mac地址)

增加了tomcat直接跑的war包,配置文件里面配置

# 注意事项:
    1.写入hosts,将dl.serverspeeder.com重定向到shell顶部填写的HOSTADDR(这里就靠自己部署了,反正就是返回一个code:200,让ss认为lic是正常的,部署好不要忘了在hosts里面修改dl.serverspeeder.com,我默认写127.0.0.1了)
注意事项: 需要把项目放在Tomcat-webapps-ROOT来运行,因为软件请求的时候地址是http://***.com/ac.do,或者通过nginx代理也可以<br>

# 接口使用提示
    1.lic生成,100M带宽默认: http://ip.com[:port]/regenspeeder/lic?mac=00:00:00:00:00:00
    2.lic生成指定日期: http://ip.com[:port]/regenspeeder/lic?mac=00:00:00:00:00:00&expires=2035-12-31
    3.lic生成指定带宽: http://ip.com[:port]/regenspeeder/lic?mac=00:00:00:00:00:00&bandwidth=100M
    4.生成日期参数和带宽参数可同时使用(废话...),带宽不填默认100M
    5.shell包下载: http://ip.com[:port]/serverspeeder/servspdShell.tar.gz
# 使用方法
    1.在服务器上安装tomcat ubuntu为apt-get install tomcat7
    2.将仓库里srcANDwar里的servspd.war放到tomcat里面webapps包中(默认tomcat7的webapps目录是/var/lib/tomcat7/webapps),最好重命名成ROOT,这样网址中不需要加项目名,tomcat端口最好为80,也可以使用nginx进行反向代理,
    3.测试使用:ROOT http://您的服务器ip[:服务器端口]/
    非ROOT: http://您的服务器IP[:服务器端口]/servspd/
    4.如果显示一个 Hello World 字样就可以了
    5.打开servspdInstaller.sh 修改HOST=http://ip.com[:port]为自己服务器ip和项目名 例如HOST=http://10.1.1.1:8080/servspd
    6.额外:如果tomcat是80端口,且项目已经重命名成ROOT,则打开servspdInstaller.sh 修改HOSTADDR=[hostIP]为自己服务器ip 例如HOSTADDR=10.1.1.1
    7.将servspdInstaller.sh传到服务器上,输入 bash servspdInstaller.sh 即可进行自动安装
项目为java servlet项目,Eclipse Project<br>

### 需要自行部署eclipse项目,来重定向ss的定时lic检测,否则会因为无法更新lic而导致ss加速无效
## 此软件仅供交流和学习使用, 不得用于其他非法用途, 使用后请自觉删除