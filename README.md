# Scoop安装和使用指南

推荐博客：https://www.limufang.com/post/569.html

## 1、Scoop介绍

Scoop是一款适用于Windows平台的命令行软件（包）管理工具，这里是[Github介绍页](https://link.zhihu.com/?target=https%3A//github.com/ScoopInstaller/Scoop)。简单来说，就是可以通过命令行工具（PowerShell、CMD等）实现软件（包）的安装管理等需求，**通过简单的一行代码实现软件的下载、安装、卸载、更新等操作**。其灵感来源于macOS的[Homebrew](https://link.zhihu.com/?target=https%3A//github.com/Homebrew/brew)，Mac用户可以去了解了解。

## 2、安装和使用

1.  在管理员的powershell下进行操作

2. 设置访问权限：Set-ExecutionPolicy RemoteSigned -scope CurrentUser 

   ![image-20220706232950160](https://github.com/kotiler/Scoop/tree/main/README-IMG/1.png)

3. 设置Scoop的位置：（两种方式）

   ```
   //第一种方式
   $env:SCOOP='D:\Scoop'
   [Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
   ```

   ```
   //第二种方式
   $env:SCOOP='D:\Scoop'
   [Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')//全局安装的路径，推荐，因为某些软件下载需要管理员权限
   ```

4. 开始安装：（两种方式，从官网下载安装，或者从国内镜像网址下载安装）

   ```
   //官网下载安装
   irm get.scoop.sh | iex
   ```

   ```
   //国内镜像网址下载安装（当从官网下载安装失败后就用这个，这里提供三个镜像地址，任选其一即可）
   iwr -useb https://gitee.com/RubyKids/scoop-cn/raw/master/install.ps1 | iex
   或者：
   iwr -useb https://gitee.com/glsnames/scoop-installer/raw/master/bin/install.ps1 | iex
   或者
   iex (new-object net.webclient).downloadstring('https://raw.githubusercontent.com/lukesampson/scoop/master/bin/install.ps1')        //我用的是这个
   ```

   ![image-20220706232906985](https://github.com/kotiler/Scoop/tree/main/README-IMG/2.png)

   ![image-20220707101857389](https://github.com/kotiler/Scoop/tree/main/README-IMG/3.png)

5. 使用scoop config proxy 127.0.0.1:10809将端口配置成vpn的端口（10809：这里是我自己的端口），因为scoop update更新自己需要在官网下载，需要配置成vpn的端口，或者要设置vpn为全局代理。

6. 如果使用scoop config proxy 127.0.0.1:10809更改了端口配置，想要恢复默认的，那么就要在用户名的config文件夹中删除掉scoop的配置文件。如下：

   ![image-20220707101157747](https://github.com/kotiler/Scoop/tree/main/README-IMG/4.png)

   

7. 安装好后可以在命令行输入scoop检查下是否安装成功。

8. scoop update：安装好后可以用这个命令来更新自己（如果不使用scoop config proxy 127.0.0.1:10809来配置端口或者设置全局代理，那么会出错）。

   ![image-20220707105009350](https://github.com/kotiler/Scoop/tree/main/README-IMG/5.png)

   ![image-20220707102331955](https://github.com/kotiler/Scoop/tree/main/README-IMG/6.png)

9. 安装应用，首先安装git：scoop install git

   ![image-20220706234056304](https://github.com/kotiler/Scoop/tree/main/README-IMG/7.png)

10. 安装好后就可以在设定的位置看到Scoop文件夹了，内部相关文件夹的作用如下：

    * apps——所有通过scoop安装的软件都在里面。

    - buckets——管理软件的仓库，用于记录哪些软件可以安装、更新等信息，默认添加`main`仓库，主要包含无需GUI的软件，可手动添加其他仓库或自建仓库，具体在[推荐软件仓库](https://zhuanlan.zhihu.com/write#推荐软件仓库)中介绍。
    - cache——软件下载后安装包暂存目录。
    - persit——用于储存一些用户数据，不会随软件更新而替换。
    - shims——用于软链接应用，使应用之间不会互相干扰，实际使用过程中无用户操作不必细究。

11. 其他命令：

    ```
    scoop search：查看所有可安装的应用
    scoop search qq：查看是否有某个应用
    ```

12. 默认是安装第一个软件包的应用，如果想安装其他软件包的可以使用前缀区分：如下

    至于如何添加软件源，稍后再讲 

![image-20220707110245854](https://github.com/kotiler/Scoop/tree/main/README-IMG/8.png)

13. 添加更多的软件包  

    ```
    bucket：软件包的别名，里面定义了我们可以安装哪些软件
    命令如下：
    scoop help bucket：该命令展示了关于bucket的命令
    scoop bucket known：该命令展示了官方推荐的一些软件包
    scoop bucket add extras：添加软件包（extras是软件包的名字）
    //添加第三方软件包 
    scoop bucket add raresoft https://github.com/L-Trump/scoop-raresoft  （raresoft是软件包名，后面的是github地址）
    ```

    ![image-20220707111021431](https://github.com/kotiler/Scoop/tree/main/README-IMG/9.png)

14. 软件包网址推荐：

    ```
    scoop的git官网：https://github.com/ScoopInstaller/Scoop
    
    一些github网址：https://github.com/tapannallan/awesome-scoop或者https://github.com/ScoopInstaller/awesome
    
    一些破解版软件包网址：https://github.com/LstHeart/scoop-raresoft
    ```

