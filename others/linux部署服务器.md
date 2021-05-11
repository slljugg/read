选取服务器  由于大多数服务器无法使用，采用了阿里云。
    ：选着好服务器后给服务器会给你一个公网ip xx.xx.xx.xx和一个私网ip xxx.xxx.xxx.xxx   （两者的区别是公网ip外部可以访问你私网ip外部无法访问）。选着公网ip作为服务器ip。
    >打开gitbash  >ssh root@xx.xx.xx.xx(公网ip) 
    连接成功后输入服务器密码（服务器密码没有的话可以让服务器重置密码） ，第一次登录会询问你是否将电脑指纹显示安全选择yes
    输入密码后就成功连接上远程服务器了。  如果之后重装系统一定去.ssh文件夹里面known_hosts里面将指纹擦除，要不无法登录。

    curl api,ipify.org  显示ip的指令（linux）

    每次使用密码登录比较麻烦   生成公私钥 ssh-keygen(git环境下)  然后ssh-copy-id  root@xx.xx.xx.xx让复制的id去打开服务器
    钥为公钥。

    同时git push的时候也可以使用这个钥匙填入ssh处，这样每次push的时候就不用了输入密码。

    在linux环境下输入  在主目录.ssh文件下有一个文件authorized_keys   该文件内存放的就是信任的公钥列表，上面就是将公钥放进这个文件里。

    每次输入ssh root@xx.xx.xx.xx(公网ip)（git）登录服务器很麻烦，可以在git环境下>cd （进入文档）  > ls.a（显示文件）其中有一个.bashrc的文件，该文件表示每次进入git时候需要初始化的操作。 进入该文件  vi .bashrc  在该文件中添加一句话alias 8 ="ssh root@xx.xx.xx.xx"  保存退出：wq  w保存  q退出   该操作相当于将8这个数字代替了那句话。

    vi /etc/ssh/sshd_config(linux)  里面可以更改好多默认项目，端口。。
    例如阿里云有一个设置长时间不联系服务器会给你中断
      
      #ClientAliveInterval 0
      #ClientAliveInterval 3   将这两项分别修改为
      
      #ClientAliveInterval 30
      #ClientAliveInterval 86400
      两项分别代表
      ：客户端每隔多少秒向服务发送一个心跳数据
      ：客户端多少秒没有相应，服务器自动断掉连接

      重启sshd服务service sshd restart
      再次进入就不会没用操作就马上断开
    
    
    
    
    linux退出操作指令：exit
    在config中退出指令为:q  :wq(保存后退出) :q!(强制退出)
    安装：apt install xxx
    删除文件：rm 文件
    删除文件夹： rmdir 文件夹
    强制删除：rm -rf 文件或者文件夹
    暂停任务：ctrl + z
    后台继续执行任务：bg
    将后台任务转向前台：fg
    当前任务查看：jobs
    重启linux系统：sudo reboot

    开始部署服务器内部软件：
      node.js :
        网页打开node.js的官网。 在下方有一个other downloads（其他下载（在最新版下方）） 点开链接
      在链接下方选择使用安装包安装node.js展开链接。选对应操作系统。点击packages下方的链接进入。再选着对应操作系统。下拉找到想安装的node.js版本。按照操作系统复制安装语句到linux环境下粘贴安装语句。（一般都是两句话）安装后使用node -v查看安装版本。npm -v查看附带的npm版本。  


      shell:linux自带的是bash  bash虽然强大，但是还是不够操作简单化，下面两款操作更加简单
      fish:
        安装fish:  apt install fish    安装后输入fish就会进入fish操作指令中，fish是一个方便cd文件夹的脚本
      
      zsh:
        安装zsh之前一定要保证安装了git   没有安装的话安装git   apt install git
        安装zsh：  apt install zsh   安装后输入zsh就回进入zsh操作指令中，zsh是一个方便很多操作的脚本，网页上还有很多优化的更加优化的版的zsh    其中oh my zsh最为广泛，网页搜索oh my zsh   https://github.com/ohmyzsh/ohmyzsh   找到这句话sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"  粘贴到zsh环境下。在cd下 l可以看见一个文件.zshrc   进入该文件内 vi .zshrc可以改变zsh的主题  选项 ZSH_THEME="xxxx"  ,我选择的是ys报错后退出：wq。
        更改主题后服务器地处不同地方会有时差，可以搜索修改时差https://www.cnblogs.com/h2appy/archive/2008/11/27/1342029.html     选着该句：cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
      
  文本编辑器：
    mc&mcedit
      apt install mc   安装后就可以进入mc  查看文件  输入exit退出  或者点击quit退出
      安装mc后mcedit是携带的  使用mcedit foo.js就可以创建foo文件  点击quit退出 创建的文件可以使用 rm foo.js删除

  任务管理器：
    top
      不用安装系统自带   进入后按q退出   使用不方便
    htop
      安装apt install htop   输入htop进入任务管理器   想关闭哪个进程点击进程然后点击kill  或者  enter强制关闭。 点击quit退出或者按键Q
  
  文件传输 （git环境下）
      git clone https://github.com//slljugg/slljugg.github.io
      scp 
        用法： 
        scp 文件（要在这个文件所在文件夹打开gitbash）   root@xx.xx.xx.xx:~/     将文件传输到远程服务器的当前文档内

        不是固定端口时要用-p显示端口来传输      
        scp -P 文件A（要在这个文件所在文件夹打开gitbash）   root@xx.xx.xx.xx:~/    将文件传输到远程服务器的当前文档内
        
        远程反过来也是成立的：
        scp root@xx.xx.xx.xx:~/文件A    ./    将远程当前文档下的文件A传输到当前荡开gitbash的文件夹内

        传文件夹也是一样的：多了-r
        scp -r ./文件夹（要在这个文件所在文件夹打开gitbash）   root@xx.xx.xx.xx:~/     将文件夹传输到远程服务器的当前文档内
      
      filezilla：（外部文件）    sftp：//基于ssh的文件传输协议

  命令行窗口管理器：tmux  安装apt install tmux
      水平方向切割 ctrl + b  然后 shift + 5（%）相当于按百分号
      垂直方向切割 ctrl + b  然后shift + ' (") 相当于按双引号
      鼠标移动  ctrl + b 然后方向键
      退出exit
      后台运行 crlt + b  然后 d
      返回前台 tmux a  (退出后仍然可行)
      打开鼠标功能：  可以直接使用鼠标，省去上面键盘操作  vi .tmux.conf   进入tmux的配置文件   添加一句： set -g mouse on 
                    保存退出：wq
      新建窗口： ctrl + b  然后 c


  进程管理工具(node.js)
    pm2 ：安装 npm i -g pm2
    指令：
        pm2 start aaa.js  相当于帮你用nodejs启动该文件并且在不stop的情况下退出会继续使用。
        退出后想继续查看管理的进程  pm2 l
        想具体查看哪个进程  pm2 show id(id号)
        停止某个进程 pm2 stop id
        停止全部进程 pm2 stop 
        开始某个进程 pm2 restart id
        开始全部进程 pm2 restart all
        查看快捷键 pm2 -h
        查看进程输出 pm2 log 
        保存当前任务  pm2 save
        重启关机前的任务 pm2 resurrect
        加入到自启动项目 pm2 startup
        退出自启动项目  pm2 unstartup

  http  加证书 成为https
      先安装搜索acme.sh   https://github.com/acmesh-official/acme.sh   找到 
      curl https://get.acme.sh | sh -s email=my@example.com  在命令行输入  安装完成后  退出重进会有acme.sh命令

      添加s    acme.sh --issue --standalone -d example.com（自己的域名）