
# {{Paj.Toe}}

网络架构和协议规范是必不可少的,但是一个好的蓝图不足以解释Internet的巨大成功: 连接到Internet的计算机的数目在几乎30年间呈指数增长 (尽管现在很难得到精确的数字) . 通过) 据估计,2009年互联网用户数量约为18亿,占世界人口的百分比令人印象深刻. 

互联网成功的原因是什么?当然有许多促成因素 (包括好的体系结构) ,但是使因特网如此成功的一个原因是,它的许多功能是由运行在通用计算机上的软件提供的. 这样做的意义在于,新的功能可以通过"编程的小问题"轻松地添加. 结果,新的和服务ℴℴ电子商务ㄡ视频会议和IP电话ℴℴ以几个为例ℴℴ以令人难以置信的速度出现. 

相关因素是商品机器中计算能力的大量增加. 虽然计算机网络在原理上总是能够传输任何类型的信息,例如数字语音样本ㄡ数字化图像等,但是如果计算机发送和接收数据太慢而无法做任何有用的事情,那么这种潜力就不特别有趣. 有了这些信息. 实际上,当今所有的计算机都能够全速播放数字化语音,并能够以对一些 (但不是全部) 应用程序有用的速度和分辨率显示视频. 因此,今天的网络越来越多地用于承载多媒体,并且它们对多媒体的支持只会随着计算硬件变得更快而提高. 

自本书第一版问世以来,网络应用程序的编写已经成为一个更加主流的活动,而仅仅对少数专家来说就不再是一项工作了. 许多因素都起到了这种作用,包括使非专家工作更容易的更好的工具,以及开拓新的市场,如智能手机的应用程序. 

需要注意的一点是,知道如何实现网络软件是理解计算机网络的重要部分,虽然您不会被要求实现像IP这样的低级协议,但是您很有可能找到实现应用程序级协议的理由. 难以捉摸的"杀手级应用",这将导致难以想象的名利. 首先,本节介绍在Internet上实现网络应用程序所涉及的一些问题. 通常,此类程序同时是应用程序 (即,设计为与用户交互) 和协议 (即,与网络上的对等方通信) . 

## 应用程序编程接口 (套接字) 

在实现网络应用程序时启动的地方是由网络导出的接口. 由于大多数网络协议的软件 (特别是那些高协议栈) ,几乎所有的计算机系统实现网络协议作为操作系统的一部分,当我们将接口的网络出口,"我们一般是指界面,THOS提供给它的网络子系统. 这个接口通常被称为网络. *应用程序编程接口* (API) . 

虽然每个操作系统自由定义自己的网络API (大部分) ,这些在一定时间的API已经成为广泛的支持;那就是,他们已经被移植到其他的比他们的本地系统的操作系统. 这就是发生了什么事*插座接口*最初由UNIX的伯克利分布提供,它现在在几乎所有流行的操作系统中都支持,并且是特定语言接口的基础,例如Java套接字库. 优势产业的广泛支持一个单一的API,应用程序可以很容易地移植从一个操作系统,开发人员可以很容易地写出多个操作系统中的应用. 

在描述套接字接口之前,重要的是要记住两个问题. 每个协议提供了一组特定的*服务*,API提供了一个*句法*通过这些服务可以在特定的计算机系统上调用这些服务. 然后,实现负责将API定义的操作和对象的有形集合映射到协议定义的抽象服务集合. 如果您已经很好地定义了接口,那么就可以使用接口的语法来调用许多不同协议的服务. 这种通用性当然是套接字接口的一个目标,尽管它还远远不够完善. 

Socket接口的主要抽象,这并不奇怪,是*插座*. 一个好的方法来考虑一个套接字是本地应用程序连接到网络的一个点. 该接口定义了创建套接字ㄡ将套接字附加到网络ㄡ通过套接字发送/接收消息和关闭套接字的操作. 为了简化讨论,我们将限制显示如何使用套接字与TCP. 

第一步是创建一个套接字,这是通过以下操作完成的: 

```c
int socket(int domain, int type, int protocol)
```

这个操作需要三个参数的原因是套接字接口被设计成足够通用以支持任何底层协议套件. 具体来说,`domain`参数指定协议*家庭*这将被使用: `PF_INET`表示互联网族,`PF_UNIX`表示UNIX管道设施,以及`PF_PACKET`表示对网络接口的直接访问 (即,它绕过TCP/IP协议栈) . 这个`type`参数指示通信的语义. `SOCK_STREAM`用于表示字节流. `SOCK_DGRAM`是一种表示面向消息的服务的替代方案,如UDP提供的服务. 这个`protocol`参数标识要使用的特定协议. 在我们的例子中,这个论点是`UNSPEC`因为组合`PF_INET`和`SOCK_STREAM`意味着TCP. 最后,返回值从`socket`是一个*手柄*对于新创建的Socket,它是我们将来可以引用套接字的标识符. 它作为对这个套接字的后续操作的一个参数. 

下一步取决于您是客户机还是服务器. 在服务器机器上,应用程序执行*被动的*打开服务器说它准备接受连接,但实际上并不建立连接. 服务器通过调用以下三个操作来实现这一点: 

```c
int bind(int socket, struct sockaddr *address, int addr_len)
int listen(int socket, int backlog)
int accept(int socket, struct sockaddr *address, int *addr_len)
```

这个`bind`操作,顾名思义,绑定新创建的`socket`到指定`address`. 这是网络地址*地方的*参与服务器. 注意,当与互联网协议一起使用时,`address`是包含服务器的IP地址和TCP端口号的数据结构. 端口用于间接标识进程. 它们是一种形式. *解复用键*.  端口号通常是特定于所提供的服务的一些公知号码;例如,Web服务器通常接受端口80上的连接. 

这个`listen`然后,操作定义在指定的连接上可以挂起多少个连接. `socket`. 最后,`accept`操作实行被动开放. 它是一个阻塞操作,直到远程参与者建立了连接才返回,当它完成时,返回*新的*与此刚刚建立的连接相对应的Socket,以及`address`参数包含*遥远的*参加者的地址. 注意什么时候`accept`返回,作为参数给出的原始套接字仍然存在,并且仍然对应于被动打开;它用于`accept`.

在客户端机器上,应用程序执行*积极的*打开,也就是说,它希望通过调用以下单个操作来与谁通信: 

```c
int connect(int socket, struct sockaddr *address, int addr_len)
```

此操作直到TCP成功建立连接后才返回,此时应用程序可以自由地开始发送数据. 在这种情况下,`address`包含远程参与者的地址. 在实践中,客户端通常只指定远程参与者的地址,并让系统填写本地信息. 虽然服务器通常侦听众所周知的端口上的消息,但是客户机通常并不关心它自己使用哪个端口;OS只是选择一个未使用的端口. 

一旦建立连接,应用程序进程调用以下两个操作来发送和接收数据: 

```c
int send(int socket, char *message, int msg_len, int flags)
int recv(int socket, char *buffer, int buf_len, int flags)
```

第一个操作发送给定的`message`超过指定`socket`而第二个操作从指定的消息接收消息. `socket`进入给定`buffer`. 两个操作都需要一组`flags`这控制了操作的某些细节. 

## 实例应用

现在我们展示一个简单的客户机/服务器程序的实现,它使用套接字接口通过TCP连接发送消息. 该程序还使用其他UNIX联网实用程序,我们在这里介绍. 我们的应用程序允许用户在一台机器上键入并向另一台机器上的用户发送文本. 它是UNIX的简化版本. `talk`程序,它类似于即时消息应用程序核心的程序. 

### 顾客

我们从客户端开始,它以远程机器的名称作为参数. 它调用UNIX实用工具将这个名称转换成远程主机的IP地址. 下一步是构造地址数据结构 (地址数据结构) . `sin`) 由套接字接口预期. 请注意,此数据结构指定我们将使用套接字连接到Internet (`AF_INET`) 在我们的示例中,我们使用TCP端口5432作为众所周知的服务器端口;这个端口碰巧没有分配给任何其他Internet服务. 建立连接的最后一步是调用`socket`和`connect`. 一旦操作返回,连接就建立并且客户端程序进入其主循环,主循环从标准输入读取文本并通过套接字发送. 

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#define SERVER_PORT 5432
#define MAX_LINE 256

int
main(int argc, char * argv[])
{
  FILE *fp;
  struct hostent *hp;
  struct sockaddr_in sin;
  char *host;
  char buf[MAX_LINE];
  int s;
  int len;

  if (argc==2) {
    host = argv[1];
  }
  else {
    fprintf(stderr, "usage: simplex-talk host\n");
    exit(1);
  }

  /* translate host name into peer's IP address */
  hp = gethostbyname(host);
  if (!hp) {
    fprintf(stderr, "simplex-talk: unknown host: %s\n", host);
    exit(1);
  }

  /* build address data structure */
  bzero((char *)&sin, sizeof(sin));
  sin.sin_family = AF_INET;
  bcopy(hp->h_addr, (char *)&sin.sin_addr, hp->h_length);
  sin.sin_port = htons(SERVER_PORT);

  /* active open */
  if ((s = socket(PF_INET, SOCK_STREAM, 0)) < 0) {
    perror("simplex-talk: socket");
    exit(1);
  }
  if (connect(s, (struct sockaddr *)&sin, sizeof(sin)) < 0)
  {
    perror("simplex-talk: connect");
    close(s);
    exit(1);
  }
  /* main loop: get and send lines of text */
  while (fgets(buf, sizeof(buf), stdin)) {
    buf[MAX_LINE-1] = '\0';
    len = strlen(buf) + 1;
    send(s, buf, len, 0);
  }
}
```

### 服务器

服务器同样简单. 它首先通过填写自己的端口号来构造地址数据结构 (`SERVER_PORT`) 通过不指定IP地址,应用程序愿意接受本地主机的任何IP地址上的连接. 接下来,服务器执行被动打开所涉及的初步步骤;它创建套接字,将其绑定到本地地址,并设置允许的最大挂起连接数. 最后,主循环等待远程主机尝试连接,当连接成功时,它接收并输出到达连接的字符. 

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>

#define SERVER_PORT  5432
#define MAX_PENDING  5
#define MAX_LINE     256

int
main()
{
  struct sockaddr_in sin;
  char buf[MAX_LINE];
  int len;
  int s, new_s;

  /* build address data structure */
  bzero((char *)&sin, sizeof(sin));
  sin.sin_family = AF_INET;
  sin.sin_addr.s_addr = INADDR_ANY;
  sin.sin_port = htons(SERVER_PORT);

  /* setup passive open */
  if ((s = socket(PF_INET, SOCK_STREAM, 0)) < 0) {
    perror("simplex-talk: socket");
    exit(1);
  }
  if ((bind(s, (struct sockaddr *)&sin, sizeof(sin))) < 0) {
    perror("simplex-talk: bind");
    exit(1);
  }
  listen(s, MAX_PENDING);
  
 /* wait for connection, then receive and print text */
  while(1) {
    if ((new_s = accept(s, (struct sockaddr *)&sin, &len)) < 0) {
      perror("simplex-talk: accept");
      exit(1);
    }
    while (len = recv(new_s, buf, sizeof(buf), 0))
      fputs(buf, stdout);
    close(new_s);
  }
}
```
