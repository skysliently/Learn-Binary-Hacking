sockopt系列调用
========================================

setsockopt
----------------------------------------
setsockopt用于任意类型、任意状态套接口的设置选项值，函数原型为 ``int setsockopt(int s, int level, int optname, void* optval, socklen_t* optlen);`` 。

getsockopt
----------------------------------------
函数原型为 ``int getsockopt(int sock, int level, int optname, void *optval, socklen_t *optlen);`` 。

参数说明
----------------------------------------
选项为：

- sockfd 标识一个套接口的描述字
- level 选项定义的层次，定义在 ``include/linux/socket.h`` 中
    - SOL_IP 0
    - SOL_SOCKET 通用套接字选项
    - IPPROTO_TCP TCP选项
    - IPPROTO_IP IP选项
    - IPPROTO_IPV6
- optname 需设置的选项，定义在 ``include/uapi/linux/in.h`` 中
- optval 指向存放选项待设置的新值的缓冲区的指针
- optlen optval缓冲区长度

其中SOL_IP为 `SOL_IP` 时，对应的选项如下：

- IP_MULTICAST_TTL 设置多播组数据的TTL值
- IP_ADD_MEMBERSHIP 在指定接口上加入组播组
- IP_DROP_MEMBERSHIP 退出组播组
- IP_MULTICAST_IF 获取默认接口或设置接口
- IP_MULTICAST_LOOP 禁止组播数据回送

对于SOL_IP为 `SOL_SOCKET` 时，对应的选项如下：

+---------------+------------------------+----------------+
| 选项值        | 选项含义               | 数据类型       |
+===============+========================+================+
| SO_BROADCAST  | 允许发送广播数据       | int            |
+---------------+------------------------+----------------+
| SO_DEBUG      | 允许调试               | int            |
+---------------+------------------------+----------------+
| SO_DONTROUTE  | 不查找路由             | int            |
+---------------+------------------------+----------------+
| SO_ERROR      | 获得套接字错误         | int            |
+---------------+------------------------+----------------+
| SO_KEEPALIVE  | 保持连接               | int            |
+---------------+------------------------+----------------+
| SO_LINGER     | 延迟关闭连接           | struct linger  |
+---------------+------------------------+----------------+
| SO_OOBINLINE  | 带外数据放入正常数据流 | int            |
+---------------+------------------------+----------------+
| SO_RCVBUF     | 接收缓冲区大小         | int            |
+---------------+------------------------+----------------+
| SO_SNDBUF     | 发送缓冲区大小         | int            |
+---------------+------------------------+----------------+
| SO_RCVLOWAT   | 接收缓冲区下限         | int            |
+---------------+------------------------+----------------+
| SO_SNDLOWAT   | 发送缓冲区下限         | int            |
+---------------+------------------------+----------------+
| SO_RCVTIMEO   | 接收超时               | struct timeval |
+---------------+------------------------+----------------+
| SO_SNDTIMEO   | 发送超时               | struct timeval |
+---------------+------------------------+----------------+
| SO_REUSERADDR | 允许重用本地地址和端口 | int            |
+---------------+------------------------+----------------+
| SO_TYPE       | 获得套接字类型         | int            |
+---------------+------------------------+----------------+
| SO_BSDCOMPAT  | 与BSD系统兼容          | int            |
+---------------+------------------------+----------------+

其中SOL_IP为 `IPPROTO_IP` 时，对应的选项如下：

- IP_HDRINCL：在数据包中包含IP首部
- IP_OPTINOS：IP首部选项
- IP_TOS：服务类型
- IP_TTL：生存时间

其中SOL_IP为 `IPPRO_TCP` 时，对应的选项如下：

- TCP_MAXSEG：TCP最大数据段的大小
- TCP_NODELAY：不使用Nagle算法

返回值说明
----------------------------------------
成功执行时，返回0。失败返回-1，errno被设为以下的某个值

- EBADF：sock不是有效的文件描述词
- EFAULT：optval指向的内存并非有效的进程空间
- EINVAL：在调用setsockopt()时，optlen无效
- ENOPROTOOPT：指定的协议层不能识别选项
- ENOTSOCK：sock描述的不是套接字
