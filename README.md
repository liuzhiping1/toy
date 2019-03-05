# Toy说明文档

## Toy的简介
Toy是一个简易服务器接口开发示例的项目，里面包含了Java服务端和Android客户端的源码，还有一个可部署的服务端文件目录。服务端程序是使用IDEA构建的SpringBoot项目，无需安装Tomcat和进行复杂的配置，即可运行（服务器系统需要安装JDK）。Android客户端使OkGo框架进行网络请求。

## Toy的目录
- **server** : 服务端的源码，使用IDEA开发工具打开。
- **client** : 客户端的源码，使用Android Studio开发工具打开。
- **deploy** : 可部署的服务端文件目录，clone下来，系统上安装了JDK，通过一行命令即可跑起服务端程序。

## 服务端快速启动
一、使用git工具克隆该个仓库到本地。
```git
git clone https://github.com/mailhu/toy.git
```
二、以Windows系统为例，打开电脑上的命令行提示符，然后输入命令切换到“toy”目录中的“deploy”目录，例如我的“toy”目录放在桌面，要切换到在“deploy”目录，在命令提示符中输入的命令如下：
```cmd
cd C:\Users\Lake\Desktop\toy\deploy
```
三、在命令提示符中切换到“deploy”目录后，需要启动服务端程序，输入如下命令：
```cmd
java -jar Demo.jar
```
四、当最后一行出现“Started DemoApplication in xxx seconds”后，一般是启动成功了，命令提示符出现的界面如下：
```cmd
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-04 18:23:25.303  INFO 13828 --- [           main] com.example.demo.DemoApplication         : Starting DemoApplication on LAPTOP-55JLANPR with PID 13828 (C:\Users\Lake\Desktop\toy\deploy\Demo.jar started by Lake in C:\Users\Lake\Desktop\toy\deploy)
2019-03-04 18:23:25.306  INFO 13828 --- [           main] com.example.demo.DemoApplication         : No active profile set, falling back to default profiles: default
2019-03-04 18:23:27.497  INFO 13828 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-03-04 18:23:27.537  INFO 13828 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-04 18:23:27.538  INFO 13828 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.16]
2019-03-04 18:23:27.551  INFO 13828 --- [           main] o.a.catalina.core.AprLifecycleListener   : The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path: [C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\Windows\Sun\Java\bin;C:\Windows\system32;C:\Windows;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\NVIDIA Corporation\PhysX\Common;C:\Program Files\Intel\WiFi\bin\;C:\Program Files\Common Files\Intel\WirelessCommon\;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\Git\cmd;C:\Program Files\dotnet\;C:\Program Files\Java\jdk1.8.0_201\bin;C:\Program Files\Apache\apache-maven-3.6.0\bin;C:\Program Files\MySQL\MySQL Utilities 1.6\;C:\Users\Lake\AppData\Local\Microsoft\WindowsApps;C:\Users\Lake\AppData\Local\Programs\Microsoft VS Code\bin;C:\Program Files\Java\jdk1.8.0_201\bin;.]
2019-03-04 18:23:29.090  INFO 13828 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-04 18:23:29.090  INFO 13828 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 3718 ms
2019-03-04 18:23:29.353  INFO 13828 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-04 18:23:29.618  INFO 13828 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2019-03-04 18:23:29.622  INFO 13828 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.753 seconds (JVM running for 8.646)
```
五、在本机的浏览器的地址栏里输入如下url测试一下服务端程序。
```http
http://localhost:8080/api/test?nickname=Lake&gender=male&age=20
```
六、若服务端返回了相关的json数据，则服务端程序正常运行
```json
{"code":0,"result":"Lake's age is 20 year old, he(she) is a boy"}
```
七、以上步骤是通过“deploy”目录的文件启动服务端程序，你也可以使用IDEA打开“server”目录，导入项目，然后run起。

## 客户端测试
一、电脑和测试的手机连接同一个网络，例如WiFi。我为了测试方便，让手机开热点，电脑连接手机热点。

二、在电脑命令提示符中获取本机当前的IP地址，命令和结果如下：
```cmd
ipconfig
```
```cmd
IPv4 地址 . . . . . . . . . . . . : 192.168.43.188
```

三、然后使用Android Studio打开“client"目录，导入客户端项目。把MainActivity类的URL常量中的IP地址改为你电脑（服务器）获取到的IP地址，代码如下：
```java
private final static String URL = "http://192.168.43.188:8080/api/test";
```
四、编译Android项目，然后安装到手机上，即可进行客户端测试。

## License
```
MIT License

Copyright (c) 2019 张观湖

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```