# 1.Linux安装anaconda以及配置pytorch环境

https://blog.csdn.net/qq_46311811/article/details/123524762

按照步骤，过程中问题：

    wget https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh

---**Anaconda3-5.2.0-Linux-x86_64**--要用最新的Anaconda版本，要不然conda-V版本过低，无法conda自我更新以及进行其他更新，会报版本号“~”的错误

# 2.Linux安装jupyter notebook

https://zhuanlan.zhihu.com/p/339695941

跳过了wsl和miniconda安装

------***重点***------
    
    ###安装jupyter相关

    conda install jupyter notebook 
    python -m ipykernel install --user
    conda install -c conda-forge jupyter_contrib_nbextensions 
    conda install jupyterthemes
    分别代表安装jupyter notebook ，为环境添加内核，安装jupyter插件功能，安装jupyter主题功能


    ###jupyter的浏览器配置（若没有网址链接的话通过此）

    jupyter notebook --generate-config  ------------找配置文件

    进入文件自行搜索找到jupyter_notebook_config.py 文件（目录中）



    打开该文件，在文件中搜索找到
    #c.NotebookApp.notebook_dir = ''
    在该语句下面添加
    import webbrowser
    webbrowser.register('chrome',None,webbrowser.GenericBrowser(u'C:\\Users\\xgr\\AppData\\Local\\Google\\Chrome\\Application\\chrome.exe'))
    c.NotebookApp.browser = 'chrome'


# 3.什么是Jupyter Notebook

Jupyter Notebook是基于网页的用于交互计算的应用程序。其可被应用于全过程计算：开发、文档编写、运行代码和展示结果。——Jupyter Notebook官方介绍

这些文档是保存为后缀名为.ipynb的JSON格式文件，不仅便于版本控制，也方便与他人共享。 此外，文档还可以导出为：HTML、LaTeX、PDF等格式。

-----------------------------------
## 0.帮助

如果你有任何jupyter notebook命令的疑问，可以考虑查看官方帮助文档，命令如下：

    jupyter notebook --help

## 1.启动

### ① 默认端口启动

在终端中输入以下命令：

    jupyter notebook
执行命令之后，在终端中将会显示一系列notebook的服务器信息，同时浏览器将会自动启动Jupyter Notebook。

启动过程中终端显示内容如下：

    $ jupyter notebook
    [I 08:58:24.417 NotebookApp] Serving notebooks from local directory: /Users/catherine
    [I 08:58:24.417 NotebookApp] 0 active kernels
    [I 08:58:24.417 NotebookApp] The Jupyter Notebook is running at: http://localhost:8888/
    [I 08:58:24.417 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
注意：之后在Jupyter Notebook的所有操作，都请保持终端不要关闭，因为一旦关闭终端，就会断开与本地服务器的链接，你将无法在Jupyter Notebook中进行其他操作啦。
浏览器地址栏中默认地将会显示：http://localhost:8888。其中，“localhost”指的是本机，“8888”则是端口号。

如果你同时启动了多个Jupyter Notebook，由于默认端口“8888”被占用，因此地址栏中的数字将从“8888”起，每多启动一个Jupyter Notebook数字就加1，如“8889”、“8890”……

## ② 指定端口启动
如果你想自定义端口号来启动Jupyter Notebook，可以在终端中输入以下命令：

    jupyter notebook --port <port_number>
其中，“<port_number>”是自定义端口号，直接以数字的形式写在命令当中，数字两边不加尖括号“<>”。如：jupyter notebook --port 9999，即在端口号为“9999”的服务器启动Jupyter Notebook。

    jupyter notebook --no-browser
由于在完成上面内容时我同时启动了多个Jupyter Notebook，因此显示我的“8888”端口号被占用，最终分配给我的是“8889”。

## 2.主页面

    pwd   --------    复制该路径

    jupyter notebook --generate-config        -----------便捷获取配置文件所在路径的命令

## 4、Jupyter Notebook的基本使用

Running页面主要展示的是当前正在运行当中的终端和“ipynb”格式的笔记本。若想要关闭已经打开的终端和“ipynb”格式的笔记本，仅仅关闭其页面是无法彻底退出程序的，需要在Running页面点击其对应的“Shutdown”。

![png0](..\pic\img.png)

不同于有道云笔记的Markdown编译器，Jupyter Notebook无法为Markdown文档通过特定语法添加目录，因此需要通过安装扩展来实现目录的添加。
    
    conda install -c conda-forge jupyter_contrib_nbextensions

执行上述命令后，启动Jupyter Notebook，你会发现导航栏多了“Nbextensions”的类目，点击“Nbextensions”，勾选“Table
of Contents ⑵”

之后再在Jupyter Notebook中使用Markdown，点击下图的图标即可使用

![png1](..\pic\img_1.png)

在使用Markdown编辑文档时，难免会遇到需要在文中设定链接，定位在文档中的其他位置便于查看。

    [添加链接的正文](#自定义索引词)
    <a id=自定义索引词>跳转提示</a>

头尾之间的“跳转提示”是可有可无的。

### 爬取网址源代码

    %load URL--------------(获取网址源码)其中，URL为指定网站的地址。

### 加载本地Python文件

    %load Python文件的绝对路径

Python文件的后缀为“.py”。
“%load”后跟的是Python文件的绝对路径。
输入命令后，可以按CTRL 回车来执行命令。第一次执行，是将本地的Python文件内容加载到单元格内。此时，Jupyter Notebook会自动将“%load”命令注释掉（即在前边加井号“#”），以便在执行已加载的文件代码时不重复执行该命令；第二次执行，则是执行已加载文件的代码。

### 直接运行本地Python文件
**执行命令：**

    %run Python文件的绝对路径

或

    !python3 Python文件的绝对路径
或

    !python Python文件的绝对路径

**注意**
1.Python文件的后缀为“.py”。
2.“%run”后跟的是Python文件的绝对路径。
3.“!python3”用于执行Python
    3.x版本的代码。
4.“!python”用于执行Python
    2.x版本的代码。
5.“!python3”和“!python”属于 !shell命令 语法的使用，即在Jupyter Notebook中执行shell命令的语法。
6.输入命令后，可以按 control return 来执行命令，执行过程中将不显示本地Python文件的内容，直接显示运行结果。


### 在Jupyter Notebook中获取当前位置

    %pwd
或

    !pwd

在Jupyter Notebook中获取当前所在位置的绝对路径

---------

在Jupyter Notebook中的笔记本单元格中用英文感叹号“!”后接shell命令即可执行shell命令。

----------

### 同时使用不同版本的Python

**⑴ 在Python 3中创建Python 2内核**

**⒜ pip安装**

首先安装Python 2的ipykernel包。

    python2 -m pip install ipykernel

再为当前用户安装Python 2的内核（ipykernel）。

    python2 -m ipykernel install --user
注意：“--user”参数的意思是针对当前用户安装，而非系统范围内安装。

**⒝ conda安装**

首先创建Python版本为2.x且具有ipykernel的新环境，其中“<env_name>”为自定义环境名，环境名两边不加尖括号“<>”。

    conda create -n <env_name> python=2 ipykernel

然后切换至新创建的环境。

    Windows: activate <env_name>
    Linux/macOS: source activate <env_name>

为当前用户安装Python 2的内核（ipykernel）。

    python2 -m ipykernel install --user
注意：“--user”参数的意思是针对当前用户安装，而非系统范围内安装。

**⑵ 在Python 2中创建Python 3内核**

**⒜ pip安装**

首先安装Python 3的ipykernel包。

    python3 -m pip install ipykernel

再为当前用户安装Python 2的内核（ipykernel）。

    python3 -m ipykernel install --user

注意：“--user”参数的意思是针对当前用户安装，而非系统范围内安装。

**⒝ conda安装**

首先创建Python版本为3.x且具有ipykernel的新环境，其中“<env_name>”为自定义环境名，环境名两边不加尖括号“<>”。

    conda create -n <env_name> python=3 ipykernel

然后切换至新创建的环境。

    Windows: activate <env_name>
    Linux/macOS: source activate <env_name>

为当前用户安装Python 3的内核（ipykernel）。

    python3 -m ipykernel install --user

注意：“--user”参数的意思是针对当前用户安装，而非系统范围内安装。
**② 为不同环境创建内核**

**⑴ 切换至需安装内核的环境**

    Windows: activate <env_name>
    Linux/macOS: source activate <env_name>
注意：“<env_name>”是需要安装内核的环境名称，环境名两边不加尖括号“<>”。

**⑵ 检查该环境是否安装了ipykernel包**

    conda list
执行上述命令查看当前环境下安装的包，若没有安装ipykernel包，则执行安装命令；否则进行下一步。

    conda install ipykernel
**⑶ 为当前环境下的当前用户安装Python内核**

若该环境的Python版本为2.x，则执行命令：

    python2 -m ipykernel install --user --name <env_name> --display-name "<notebook_name>"

若该环境的Python版本为3.x，则执行命令：

    python3 -m ipykernel install --user --name <env_name> --display-name "<notebook_name>"

**注意:**
1. “<env_name>”为当前环境的环境名称。环境名两边不加尖括号“<>”。

2. “<notebook_name>”为自定义显示在Jupyter Notebook中的名称。名称两边不加尖括号“<>”，但双引号必须加。

3. “--name”参数的值，即“<env_name>”是Jupyter内部使用的，其目录的存放路径为~/Library/Jupyter/kernels/。如果定义的名称在该路径已经存在，那么将自动覆盖该名称目录的内容。

4. “--display-name”参数的值是显示在Jupyter Notebook的菜单中的名称。