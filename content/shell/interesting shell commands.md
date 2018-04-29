+++
title = "Interesting Shell Commands"
date = 2018-04-25T18:16:49+08:00
draft = false
tags = ["shell"]
categories = ["shell"]
+++

# 一些有意思的shell命令

```bash
$ printf "%x" \'$
$ printf \\x2F
```

将字符转化为16进制(%x), 十进制(%d)...
第二个命令将16进制转化为字符

```bash
$ python -m SimpleHTTPServer
$ python -m http.server
```

使用python来建立一个简易的web service用于文件传输，第一个时python2的写法，后一个是python3的写法，默认端口为8000，可以在后面直接加端口指定端口

```bash
$ nc -l localhost -p 1016
$ nc localhost 1016
$ nc -lu localhost -p 8125
$ nc -u localhost 8125
```

`gnu-netcat`软件包，使用`nc`命令监听1016端口，然后再用`nc`可以发送数据，这可以用于文件传输，做简易的聊天工具

```bash
curl -OL https://github.com/cmderdev/cmder/releases/download/v1.3.2/cmder.zip
```

`-O` 以原文件名字保存
`-L` 重定向跟踪
`-C` 断点续传，`-C -` ，自动检测断点

```bash
$ cat -n file.txt
$ nl file.txt
```

两个命令都可以显示文本内容并在行首加上行号，`nl`默认会忽略空行，而`cat`不会

```bash
curl -u admin:admin "http://grafana.saas.hand-china.com/api/admin/settings" 2>/dev/null | json_reformat
curl -u admin:admin "http://grafana.saas.hand-china.com/api/admin/settings" 2>/dev/null | python -m json.tool
curl -u admin:admin "http://grafana.saas.hand-china.com/api/admin/settings" 2>/dev/null | jq.[]
```

`yajl`软件包，`json_reformat`命令可以将标准输出的json内容格式化，以便于阅读
python的json.tool模块也可用于json格式化
`jq`有更加强大的功能，不仅可以格式化json，还可以从json中取出相应字段。

```bash
$ du -sh *
```

可以显示当前一级目录下所有目录（或文件）的大小，`-h`以人类可读的单位显示，`-s`只显示当前目录下的文件，不递归显示，`*`代表当前目录下所有文件

shell 脚本中`''`和`""`效果不同，`''`中的字符串被当作一般字符串处理，即使有`$varaible`的字符串也不会被解析，而`""`中的变量会被解析。

shell 脚本中\`\`和`$()`用于命令替换，`${}`用于变量替换，变量替换功能非常强大，有类似切片的功能

```bash
sed -i -e "s/profiler.collector.ip=172.20.0.219/profiler.collector.ip=localhost/" -e "/profiler.collector.ip=/a profiler.jvm.vendor.name=Oracle" -e "s/profiler.sampling.rate=20/profiler.sampling.rate=1/" pinpoint.config
sed -i 1d pinpoint.config
```

`-i`直接修改文件
`-e`指定多个匹配项
`s/pattern/changer/`修改匹配
`/pattern/a \line1\nline2`在匹配项后添加行，`\n`分行
`/pattern/i \line`在匹配项前添加行

```bash
xrandr -s 1366x768
```

`xrandr`用于强制修改分辨率，可以用`xrandr`命令列出可用的分辨率

```bash
$ nohup command > run.log 2>&1 &
$ nohup command &> run.log &
```

`nohup ... &`可以将程序后台运行，`&>`可以将标准输出和错误输出都重定向到文件中，`2>&1`表示将错误输出重定向到标准输出。

```bash
$ telnet towel.blinkenlights.nl
```

在终端里看《星球大战》

```bash
curl wttr.in/shanghai
```

终端下的天气预报

```bash
for code in {0..255};do
    echo -en "\e[38;05;${code}m██"
done
```

在终端中输出256色的色块

```bash
$ A=1;echo $A;{ A=2; };echo $A
1
2
$ A=1;echo $A;( A=2; );echo $A
1
1 
```

`{}`中的命令会在当前进程中执行，`()`中的命令会在子进程中执行

```bash
seq 100
```
用于生成一个1~100的序列