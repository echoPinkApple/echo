# java学习

### \*\* java学习\*\*

#### **git**

* Git branch 列出所有分支
* Git branch -r 列出所有远程分支
* Git branch -a 列出所有本地分支
* Git branch \[name] 创建新的分支
* Git checkout \[name\[ 切换到某一分支；
* Git push \[name1] \[name2] 推送name1到name2
* Git add . 添加文件
* Git merge \[name] 合并分支\[name]到当前分支
* 冲突处理：git merge 产生冲突后手动处理冲突，然后git add ;git commit -m ‘ ’ -I
* Git 标签： 记录特定阶段代码状态；git tag v0.1 (新建标签);git tag(查看标签)
* Git checkout -b \[branch name] \[tag name] 检出标签

#### **IDEA中使用git**

1. Settings 里面配置git
2. Vsc:版本控制
3. 远程仓库克隆项目：get from version control;

#### **Linux**

1. Linux特点：免费、开源、多任务、多用户；
2. Linux版本：内核版，发行版；
3. 网卡设置： cd /etc/sysconfig/netword-script; vi ifcfg-ens33; onboot=true;
4. linux常用命令：

| 命令                                                              | 解释                                  |
| --------------------------------------------------------------- | ----------------------------------- |
| ls \[-al] \[dir]                                                | 查看当前目录下的内容                          |
| pwd                                                             | 查看当前所在目录 print work directory       |
| cd                                                              | change directory                    |
| tourch                                                          | 创建文件                                |
| mkdir                                                           | 新建目录                                |
| rm                                                              | remove                              |
| Echo ‘LANG=“en\_US.utf-8”’ >> /etc/profile; Source /etc/profile | 解决乱码                                |
| Cat \[file]                                                     | 查看文件内容                              |
| Cat -n \[file]                                                  | 显示行号                                |
| more                                                            | 以分页形式显示内容                           |
| Tail -20 \[file]                                                | 显示文件末尾20行内容                         |
| tail -f \[file]                                                 | 动态显示末尾20行内容                         |
| Mkdir -p /a/b/c                                                 | 创建多级目录                              |
| rm -p \[dir]                                                    | 删除多级目录                              |
| rm test\*                                                       | 删除以test开头的文件                        |
| Rm -r                                                           | 递归删除                                |
| rm -f                                                           | 无需确认，直接删除                           |
| Cp hello.txt ./hi.txt                                           | 复制hello.txt并重新命名为hi.txt             |
| Cp -r \[dir] \[dir]                                             | 复制目录到另外一个目录                         |
| cp -r test/\* \[dir]                                            | 复制test里面所有内容到dir                    |
| mv hell.txt hi.txt                                              | 将文件改名为hi.txt                        |
| mv hello.txt test/                                              | 移动到test目录                           |
| mv hello/ hi/                                                   | 如果hi/不存在，则将hello改名为hi/；如果存在，则移动到hi/ |
| **tar \[-zcxvf] filename \[files]**                             | **.tar表示只打包 .tar.gz表示打包和压缩**        |
| -z                                                              | Gzip                                |
| -c                                                              | Create                              |
| -x                                                              | extract 解压                          |
| -v                                                              | Vebose显示命令执行过程                      |
| -f                                                              | file                                |
| tar -cvf                                                        | 打包                                  |
| tar -zcvf                                                       | 打包同时压缩                              |
| tar -xvf                                                        | 解包                                  |
| tar -zxvf                                                       | 解压                                  |
| tar -zxvf hello.tar.gz -C /test                                 | 解压到test文件夹                          |
| find \[dir] -name " \*name"                                     | 指定目录查找文件                            |
| grep hello hello.java                                           | 查找指定文件内指定字符串                        |
| systemctl stop firewalld                                        | 暂时关闭防火墙                             |
| system disable firewalld                                        | 永久关闭防火墙                             |
| Firewall-cmd--reload                                            | 立即生效                                |
| Firewall-cmd --zone=public --add-port=8080/tcp --permenent      | 开放指定端口                              |
| nohup java -jar test.jar &>hello.log &                          | 挂起程序，并将日志输出到hello.log               |



apollo部署到内网，增加配置使得通过外网可以访问

数据库新建远程连接用户

```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password'; 
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION; 
CREATE USER 'username'@'%' IDENTIFIED BY 'password'; 
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;
```

Rocketmq linux 安装启动：

github 下载项目，mvn -Prelease-all -DskipTests clean install -U

```shell
nohup sh bin/mqnamesrv -n localhost:9876 &
tail -f ~/logs/rocketmqlogs/namesrv.log
nohup sh bin/mqbroker -n localhost:9876 -c conf/broker.conf autoCreateTopicEnable=true &
tail -f ~/logs/rocketmqlogs/broker.log
sh bin/mqshutdown broker
sh bin/mqshutdown namesrv
```

Ubuntu java安装

### 安装 OpenJDK 11

在写作的时候，Java 11 是 Java 的一个长期支持版本（LTS）。它同时也是 Ubuntu 20.04的默认 Java 开发和运行环境。

以 root 或者其他 sudo 权限用户身份 运行下面的命令，更新软件包索引，并且安装OpenJDK 11 JDK 软件包：

```
sudo apt update
sudo apt install openjdk-11-jdk
```

一旦安装完成，你可以通过检查 Java 版本来验证它：

```
java -version
```

输出类似下面这样：

```
openjdk version "11.0.7" 2020-04-14
OpenJDK Runtime Environment (build 11.0.7+10-post-Ubuntu-3ubuntu1)
OpenJDK 64-Bit Server VM (build 11.0.7+10-post-Ubuntu-3ubuntu1, mixed mode, sharing)
```

就这些！此时，你已经成功地在你的 Ubuntu 系统上安装好了 Java。

JRE 被包含在 JDK 软件包中。如果你仅仅需要 JRE，安装`openjdk-11-jre`软件包。最小 Java 运行环境，安装`openjdk-11-jdk-headless`软件包。

### 三、安装 OpenJDK 8

Java 8，前一个 Java LTS 版本，目前仍被广泛应用。如果你的应用运行在 Java 8 上，你可以通过输入下面的命令，安装它：

```
sudo apt update
sudo apt install openjdk-8-jdk
```

通过检查 Java 版本，来验证安装过程：

```
java -version
```

输出将会像下面这样：

```
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1ubuntu1-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
```

### 四、设置默认版本

如果你在你的 Ubuntu 系统上安装了多个 Java 版本，你可以输入下面的命令，检测哪个版本被设置成了默认值：

```
java -version
```

想要修改默认的版本，使用`update-alternatives`命令：

```
sudo update-alternatives --config java
```

输出像下面这样：

```
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

所有已经安装的 Java 版本将会列出来。输入你想要设置为默认值的序号，并且按"Enter”。

### 五、JAVA\_HOME 环境变量

在一些 Java 应用中，环境变量`JAVA_HOME`被用来表示 Java 安装位置。

想要设置 `JAVA_HOME` 变量，首先使用`update-alternatives`找到 Java 安装路径:

```
sudo update-alternatives --config java
```

在这个例子中，安装路径如下：

* OpenJDK 11 is located at `/usr/lib/jvm/java-11-openjdk-amd64/bin/java`
* OpenJDK 8 is located at `/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java`

一旦你发现你偏好的 Java 安装路径，打开`/etc/environment`文件：

```
sudo nano /etc/environment
```

假设你想设置 `JAVA_HOME` 指定到 OpenJDK 11，在文件的末尾，添加下面的行：

```
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```

想要让修改在当前 shell 生效，你可以登出系统，再登入系统，或者运行下面的命令：

```
source /etc/environment
```

验证 `JAVA_HOME` 环境变量被正确设置：

```
echo $JAVA_HOME
```

你应该可以看到 Java 安装路径：

```
/usr/lib/jvm/java-11-openjdk-amd64
```

### 六、卸载 Java

你可以使用 apt 卸载 Java，就像卸载任何软件包一样。

例如，想要卸载`default-jdk`软件包，输入：

```
sudo apt remove openjdk-11-jdk
```

防火墙

```
sudo ufw allow smtp　      #允许所有的外部IP访问本机的25/tcp (smtp)端口 
sudo ufw allow 22/tcp      #允许所有的外部IP访问本机的22/tcp (ssh)端口 
sudo ufw allow 53          #允许外部访问53端口(tcp/udp) 
sudo ufw allow from 192.168.1.100 #允许此IP访问所有的本机端口 
sudo ufw allow proto udp 192.168.0.1 port 53 to 192.168.0.2 port 53 
sudo ufw deny smtp         #禁止外部访问smtp服务 
sudo ufw delete allow smtp #删除上面建立的某条规则 
```

lsof -i port 查看端口使用情况



#### JVM参数

Xms 起始内存

Xmx 最大内存

Xmn 新生代内存

Xss 栈大小。 就是创建线程后，分配给每一个线程的内存大小

\-XX:NewRatio=n:设置年轻代和年老代的比值。如:为3，表示年轻代与年老代比值为1：3，年轻代占整个年轻代年老代和的1/4

\-XX:SurvivorRatio=n:年轻代中Eden区与两个Survivor区的比值。注意Survivor区有两个。如：3，表示Eden：Survivor=3：2，一个Survivor区占整个年轻代的1/5

\-XX:MaxPermSize=n:设置持久代大小

收集器设置 -XX:+UseSerialGC:设置串行收集器 -XX:+UseParallelGC:设置并行收集器 -XX:+UseParalledlOldGC:设置并行年老代收集器 -XX:+UseConcMarkSweepGC:设置并发收集器 垃圾回收统计信息 -XX:+PrintGC -XX:+PrintGCDetails -XX:+PrintGCTimeStamps -Xloggc:filename 并行收集器设置 -XX:ParallelGCThreads=n:设置并行收集器收集时使用的CPU数。并行收集线程数。 -XX:MaxGCPauseMillis=n:设置并行收集最大暂停时间 -XX:GCTimeRatio=n:设置垃圾回收时间占程序运行时间的百分比。公式为1/(1+n) 并发收集器设置 -XX:+CMSIncrementalMode:设置为增量模式。适用于单CPU情况。 -XX:ParallelGCThreads=n:设置并发收集器年轻代收集方式为并行收集时，使用的CPU数。并行收集线程数。

#### Java int 类型

对于-128到127之间的数, Integer直接从数组中取, 故a1, a2指向的是同一个对象, A正确.

其余都是new出来的对象, 显然地址都不相同.

int类型与Integer类型比较时, 先将Integer拆箱, 再比较值, 故B正确.

#### java初始化的加载顺序为：

父类静态成员变量 父类静态代码块 子类静态成员变量 子类静态代码块 父类非静态成员变量，父类非静态代码块，父类构造函数，子类非静态成员变量，子类非静态代码块，子类构造函数

#### java 内存模型

A.程序计数器是一块较小的内存空间，它的作用可以看做是当前线程所执行的字节码的信号指示器（偏移地址），Java编译过程中产生的字节码有点类似编译原理的指令，程序计数器的内存空间存储的是当前执行的字节码的偏移地址，每一个线程都有一个独立的程序计数器（**程序计数器的内存空间是线程私有的**），因为当执行语句时，改变的是程序计数器的内存空间，因此它不会发生内存溢出 **，并且程序计数器是jvm虚拟机规范中唯一一个没有规定 \*OutOfMemoryError\* 异常 的区域；**

B.java虚拟机栈：**线程私有**，生命周期和线程一致。描述的是 Java 方法执行的内存模型：每个方法在执行时都会床创建一个栈帧(Stack Frame)用于存储局部变量表、操作数栈、动态链接、方法出口等信息。每一个方法从调用直至执行结束，就对应着一个栈帧从虚拟机栈中入栈到出栈的过程。 **没有类信息，类信息是在方法区中**

C.java堆：对于绝大多数应用来说，这块区域是 JVM 所管理的内存中最大的一块。**线程共享**，主要是存放对象实例和数组

D.方法区：属于**共享内存区域**，存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。

方法区是什么？ 方法区是广义上的概念，是一个定义、标准，可以理解为Java中的接口，在Jdk6、7方法区的实现叫永久代；Jdk8之后方法区的实现叫元空间，并从JVM内存中移除，放到了直接内存中； 方法区是被所有方法线程共享的一块内存区域.

运行时常量池是什么？ 运行时常量池是每一个类或接口的常量池的运行时表示形式.

具体体现就是在Java编译后生成的.class文件中，会有class常量池，也就是静态的运行时常量池；

运行时常量池存放的位置？

运行时常量池一直是方法区的一部分，在不同版本的JDK中，由于方法区位置的变化，运行时常量池所处的位置也不一样.JDK1.7及之前方法区位于永久代.由于一些原因在JDK1.8之后彻底祛除了永久代,用元空间代替。

运行时常量池存放什么？ 存放编译期生成的各种字面量和符号引用；（字面量和符号引用不懂的同学请自行查阅） 运行时常量池中包含多种不同的常量，包括编译期就已经明确的数值字面量，也包括到运行期解析后才能够获得的方法或者字段引用。 此时不再是常量池中的符号地址了，这里换为真实地址。

运行时常量池与字符串常量池？（可能有同学把他俩搞混） 字符串常量池：在JVM中，为了减少相同的字符串的重复创建，为了达到节省内存的目的。会单独开辟一块内存，用于保存字符串常量，这个内存区域被叫做字符串常量池.

字符串常量池位置？

JDK1.6时字符串常量池，被存放在方法区中（永久代），而到了JDK1.7，因为永久代垃圾回收频率低；而字符串使用频率比较高，不能及时回收字符串，会导致导致永久代内存不足，就被移动到了堆内存中。

### jvisualvm、jconsole



netty如果没有设置2内存，会默认使用Xmx做为堆外内存，-Dio.netty.maxDirectMemory



### spring cache

For caching declaration, Spring’s caching abstraction provides a set of Java annotations:

* `@Cacheable`: Triggers cache population.
* `@CacheEvict`: Triggers cache eviction.
* `@CachePut`: Updates the cache without interfering with the method execution.
* `@Caching`: Regroups multiple cache operations to be applied on a method.
* `@CacheConfig`: Shares some common cache-related settings at class-level.

### java多线程

#### 创建线程的方式：

继承Thread，实Runnable接口，实现Callable+Future，提交任务给线程池。

#### 线程参数：

**`ThreadPoolExecutor` 3 个最重要的参数：**

- **`corePoolSize` :** 核心线程数线程数定义了最小可以同时运行的线程数量。
- **`maximumPoolSize` :** 当队列中存放的任务达到队列容量的时候，当前可以同时运行的线程数量变为最大线程数。
- **`workQueue`:** 当新任务来的时候会先判断当前运行的线程数量是否达到核心线程数，如果达到的话，新任务就会被存放在队列中。

`ThreadPoolExecutor`其他常见参数 :

1. **`keepAliveTime`**:当线程池中的线程数量大于 `corePoolSize` 的时候，如果这时没有新的任务提交，核心线程外的线程不会立即销毁，而是会等待，直到等待的时间超过了 `keepAliveTime`才会被回收销毁；
2. **`unit`** : `keepAliveTime` 参数的时间单位。
3. **`threadFactory`** :executor 创建新线程的时候会用到。
4. **`handler`** :饱和策略。关于饱和策略下面单独介绍一下。

**`ThreadPoolExecutor` 饱和策略定义:**

如果当前同时运行的线程数量达到最大线程数量并且队列也已经被放满了任务时，`ThreadPoolTaskExecutor` 定义一些策略:

- **`ThreadPoolExecutor.AbortPolicy`** ：抛出 `RejectedExecutionException`来拒绝新任务的处理。
- **`ThreadPoolExecutor.CallerRunsPolicy`** ：调用执行自己的线程运行任务，也就是直接在调用`execute`方法的线程中运行(`run`)被拒绝的任务，如果执行程序已关闭，则会丢弃该任务。因此这种策略会降低对于新任务提交速度，影响程序的整体性能。如果您的应用程序可以承受此延迟并且你要求任何一个任务请求都要被执行的话，你可以选择这个策略。
- **`ThreadPoolExecutor.DiscardPolicy`** ：不处理新任务，直接丢弃掉。
- **`ThreadPoolExecutor.DiscardOldestPolicy`** ： 此策略将丢弃最早的未处理的任务请求。





```java
//spring 扩展消息转换器不生效解决方法：开启允许重复模块注册，注册完毕后关闭允许重复模块注册
// objectMapper.disable(MapperFeature.IGNORE_DUPLICATE_MODULE_REGISTRATIONS);
@Override
public void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
   log.info("扩展消息转换器");
   MappingJackson2HttpMessageConverter converter = new MappingJackson2HttpMessageConverter();
   ObjectMapper objectMapper = converter.getObjectMapper();
   objectMapper.disable(MapperFeature.IGNORE_DUPLICATE_MODULE_REGISTRATIONS);
   converter.setObjectMapper(new JacksonObjectMapper());
   converters.add(0,converter);
   objectMapper.enable(MapperFeature.IGNORE_DUPLICATE_MODULE_REGISTRATIONS);
}
```

## Linux设置开机启动的三种方法

### 方法一 添加命令

编辑文件 /etc/rc.local

```javascript
vim /ect/rc.local
```

复制

/ect/rc.local和/ect/rc.d/rc.local是软链接关系

```javascript
chmod +x /ect/rc.d/rc.local
```

复制

### 方法二 添加脚本

自己写一个shell脚本 将写好的脚本（.sh文件）放到目录 /etc/profile.d/ 下，系统启动后就会自动执行该目录下的所有shell脚本。

```javascript
cd /etc/profile.d/
```

复制

添加脚本 srs.sh

```javascript
#!/bin/sh

cd /usr/local/srs2
nohup ./objs/srs -c conf/z.conf>./log.txt &
```

复制

### 方法二 添加服务

添加文件 新建/etc/init.d/srs.sh 文件





## redis 集群搭建

```shell
#创建容器 
docker create --name redis-node01 --net host -v /data/redis-data/node01:/data -v /data/redis-data/node01/redis.conf:/usr/local/etc/redis/redis.conf -p 6379:6379 redis:latest --cluster-enabled yes --cluster-config-file nodes-node-01.conf --port 6379 --protected-mode no
docker create --name redis-node02 --net host -v /data/redis-data/node02:/data -v /data/redis-data/node02/redis.conf:/usr/local/etc/redis/redis.conf redis:latest --cluster-enabled yes --cluster-config-file nodes-node-02.conf --port 6380 --protected-mode no
docker create --name redis-node03 --net host -v /data/redis-data/node03:/data -v /data/redis-data/node03/redis.conf:/usr/local/etc/redis/redis.conf redis:latest --cluster-enabled yes --cluster-config-file nodes-node-03.conf --port 6381 --protected-mode no



docker create --name redis-node01 -v /data/redis-data/node01:/data -p 6379:6379 redis:latest --cluster-enabled yes --cluster-config-file nodes-node-01.conf 
docker create --name redis-node02 -v /data/redis-data/node02:/data -p 6379:6379 redis:latest --cluster-enabled yes --cluster-config-file nodes-node-02.conf
docker create --name redis-node03 -v /data/redis-data/node03:/data -p 6379:6379 redis:latest --cluster-enabled yes --cluster-config-file nodes-node-03.conf 


#启动容器 
docker start redis-node01 redis-node02 redis-node03
#进入redis-node01容器进行操作 
docker exec -it redis-node01 /bin/bash
redis-cli --cluster create 172.27.0.1:6379 172.27.0.1:6380 172.27.0.1:6381 --cluster-replicas 0
redis-cli --cluster create 127.0.0.1:6379 127.0.0.1:6380 127.0.0.1:6381 --cluster-replicas 0
```





## instanceof 关键字

instanceof 严格来说是Java中的一个双目运算符，用来测试一个对象是否为一个类的实例，用法为：

```java
boolean result = obj instanceof Class
```

　　其中 obj 为一个对象，Class 表示一个类或者一个接口，当 obj 为 Class 的对象，或者是其直接或间接子类，或者是其接口的实现类，结果result 都返回 true，否则返回false。

　　注意：编译器会检查 obj 是否能转换成右边的class类型，如果不能转换则直接报错，如果不能确定类型，则通过编译，具体看运行时定。
