---
title: Docker日志大小限制和切换存储目录
date: 2023-03-28 11:35:16
categories: [技术]
tags: [Docker,运维]
---

产品的各种环境使用了很多 `CentOS` 虚拟机，默认情况下 `root` 目录空间是 50 G，随着使用时间越来越长，空间会变得不够用。
<!--more-->
一直采用的方法就是清除无用的镜像和 `Docker` 日志，服务器就一直处于可用的状态。直到连清理都没用的时候，才想起来要要需找其他的方法。

当没有逼到绝境的时候，我们会习惯性依赖自己熟悉的方法和工具，可能不高效，但能解决问题，这种又不是不能用的思维害人不浅，会让人呆在舒适区不愿意出来。

上面所说的其他的方法其实很简单，就是限制 `Docker` 日志大小和将 `Docker` 数据目录切换到外部存储中。

## 日志限制

1、编辑 Docker 的配置文件 `/etc/docker/daemon.json`，如果该文件不存在，就新建一个。

```
 sudo vi /etc/docker/daemon.json
```

2、在该文件中添加以下内容，以限制单个日志文件的大小为100MB，并保留最近5个日志文件。这里我们使用 `max-size` 和 `max-file` 参数来控制日志的大小和数量。

```
{
    "log-driver": "json-file",
    "log-opts": {
      "max-size": "100m",
      "max-file": "5"
    }
}
```

* max-size：单个日志文件的最大大小；
* max-file：最多保留几个日志文件，当单个文件的日志大小超过设置后，会产生新的日志文件。

3、重新启动 `Docker` 服务使配置生效。

```
sudo systemctl restart docker
```

## 数据目录切换

在 `CentOS` 中，`Docker` 默认的目录为 `/var/lib/docker` ，可以使用 `Docker` 配置文件中的 `data-root` 选项，进行 `Dcoker` 数据目录的设置，具体步骤如下：

1、在 `/etc/docker/daemon.json`  配置文件中添加 `data-root` 选项：

```
{
    "log-driver": "json-file",
    "log-opts": {
      "max-size": "100m",
      "max-file": "5"
    }
  "data-root": "/home/docker"
}
```

* `/home/docker` 目录为外接存储，或者空间比较大的卷。

2、停用 `Docker`：

```
sudo systemctl stop docker
```

3、将 `Docker` 默认目录中的内容拷贝到新的目录中：

```
sudo rsync -aqxP /var/lib/docker/ /home/docker/ 
```

* 一个用于远程同步文件和目录的工具；
* 告诉  `rsync`  以归档模式同步文件和目录，其中  `a`  表示归档模式，  `q`  表示安静模式（不显示输出），  `x`  表示不跨越文件系统边界，  `P`  表示显示进度条和部分传输的文件。

4、修改默认目录的名称为 bak：

```
mv /var/lib/docker /var/lib/docker.bak
```

这样做的好处是可以对原始数据进行一个备份，等运行稳定了再进行删除，另外就是防止配置没有生效导致还是读取的原始目录。

5、启用 `Dcoker`：

 ```
sudo systemctl start docker
 ```

在上面第三步中使用了  `rsync`  这个命令来进行内容的同步，这个命令的含义是使用  `rsync`  工具将本地计算机中  `/var/lib/docker/`  目录下的所有文件和子目录同步到另一个本地计算机中的  `/home/docker/`  目录下。

在此之前，进行文件或目录的操作使用 `cp`  和 `scp` 比较多，这次查资料时知道了 rsync 这个命令工具，便继续学习了下和  `cp`  、 `scp`  的区别：

###  rsync 和 cp 、 rsync 的区别

* 复制方式： `cp` 和 `scp` 会将整个文件复制到目标位置，而 `rsync`只会复制需要更新的部分，这可以提高复制的速度和效率。

* 支持性： `rsync` 支持更多的操作，例如文件同步、文件备份、文件恢复等。`cp `和 `scp `仅支持文件复制。

* 传输方式：`cp` 在本地文件系统之间复制文件，`scp` 进行远程操作，而 `rsync` 可以在本地或远程机器之间进行文件同步。

* 效率：`rsync` 更有效率，因为它只复制需要更新的文件。

* 可选项：`rsync  `提供了更多的可选项和配置选项，例如压缩、部分传输、跨文件系统同步等。

总之， `rsync ` 是一个更强大、更高效的文件复制和同步工具，如果需要在本地或远程机器之间进行文件同步、备份和恢复等操作，建议使用`rsync`。而 `cp` 和 `scp` 则适用于简单的本地文件复制和远程文件传输。

## 总结

通过这次日志限制和目录切换的学习，有两点思考：

1、很多时候，更好的方式就在离你不远的地方，就看你愿不愿意往前迈一步去探寻一下，也就是说不能将就，不要有「又不是不能用」的思维，做产品、学技能都是一样；

2、工作之后的很多技能的学习都是在不断解决问题中学会的，这样会让你慢慢变得很有经验，但不系统，即便某个领域感觉已经非常熟悉了，我觉得也有必要再看看书进行系统化学习，肯定能扫出很多盲点。

共勉。

