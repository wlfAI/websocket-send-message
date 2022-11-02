# websocket-send-message
server send message , client receive message


##Required environment:

Visual Studio 2017

##实现步骤

### 1. 在vs下添加ws2_32.lib库

右键【项目】-【属性】-【链接器】-【输入】-【附加依赖项】，进行编辑，添加 ws2_32.lib库，去掉从父级或项目默认设置继承的勾选，如下图所示：

![0](https://user-images.githubusercontent.com/51230137/198981434-98d6e642-dc42-4c7f-8faf-7dfcca837b92.png)

![0](https://user-images.githubusercontent.com/51230137/198981601-f69445e5-d0b3-47b1-9379-d56660629671.png)

注意，下面的服务器端和客户端代码均写入了这一句——#pragma comment(lib, "ws2_32.lib") //加载 ws2_32.lib，因此两个程序都需要添加ws2_32.lib静态链接库。

### 2. 建立第一个项目,运行服务器端代码Sever.cpp 

在运行服务器端代码时，有的vs会出现如下错误error C4996: 'inet_addr': Use inet_pton() or InetPton() instead or define _WINSOCK_DEPRECATED_NO_WARNINGS to disable deprecated API warnings，如下图：

![0](https://user-images.githubusercontent.com/51230137/198982339-4d8df3a9-d62a-40a0-a401-8598e032f449.png)

这是因为inet_addr是一个老函数，而微软就是喜欢强迫别人用它的新函数。

【解决方案】

(1)用socket的新函数代替程序出现的所有老函数，此方法学习成本太高。

(2)在项目属性里设置,告诉编译器,我就用老函数,让她不要报错了。

所以推荐使用第二种解决方案，设置方法如下：

右键【项目】-【属性】-【配置属性】-【C/C++】-【常规】-【SDL检查】的值改为“否”，如下图：

![0](https://user-images.githubusercontent.com/51230137/198981954-0b9c810f-7894-4e7a-b164-824b725ae627.png)

### 3. 建立第二个项目,运行客户端代码Client.cpp

### 4. 运行调试
先运行 服务器端程序，再运行客户端程序，输出结果为：
Message form server: Hello World!

值得注意的是，由于这两个程序没有写入while循环，所以server 只接受一次 client 请求，当 server 向 client 传回数据后，程序就运行结束了。如果想再次接收到服务器的数据，必须再次运行 server，这只是一个非常简陋的 socket 程序，不能够一直接受客户端的请求。
