# Apache Hadoop 2.7.1 Docker image

[![DockerPulls](https://img.shields.io/docker/pulls/sequenceiq/hadoop-docker.svg)](https://registry.hub.docker.com/u/sequenceiq/hadoop-docker/)
[![DockerStars](https://img.shields.io/docker/stars/sequenceiq/hadoop-docker.svg)](https://registry.hub.docker.com/u/sequenceiq/hadoop-docker/)



_Note: this is the master branch - for a particular Hadoop version always check the related branch_

A few weeks ago we released an Apache Hadoop 2.3 Docker image - this quickly become the most [popular](https://registry.hub.docker.com/search?q=hadoop&s=downloads) Hadoop image in the Docker [registry](https://registry.hub.docker.com/).


Following the success of our previous Hadoop Docker [images](https://registry.hub.docker.com/u/sequenceiq/hadoop-docker/), the feedback and feature requests we received, we aligned with the Hadoop release cycle, so we have released an Apache Hadoop 2.7.1 Docker image - same as the previous version, it's available as a trusted and automated build on the official Docker [registry](https://registry.hub.docker.com/).

# 适合国内使用的修改

这个版本修改Dockerfile时区为中国区。考虑到中国网络下载下列文件会非常的慢，所以把所有文件全部改为自行提供，而不是通过curl的方式调用，因此需要提供几个文件在当前目录下：
* [hadoop-2.7.1.tar.gz](http://www.eu.apache.org/dist/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz)
* [hadoop-native-64-2.7.1.tgz](https://github.com/sequenceiq/docker-hadoop-build/releases/download/v2.7.1/hadoop-native-64-2.7.1.tgz)
* [jdk-7u71-linux-x64.rpm](http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.rpm)
*可以分别另寻渠道自行下载*

添加docker-compose.yml文件，添加logs映射，快速启动



_FYI: All the former Hadoop releases (2.3, 2.4.0, 2.4.1, 2.5.0, 2.5.1, 2.5.2, 2.6.0) are available in the GitHub branches or our [Docker Registry](https://registry.hub.docker.com/u/sequenceiq/hadoop-docker/) - check the tags._

# Build the image

If you'd like to try directly from the Dockerfile you can build the image as:

```
docker build  -t sequenceiq/hadoop-docker:2.7.1 .
```
# Pull the image

The image is also released as an official Docker image from Docker's automated build repository - you can always pull or refer the image when launching containers.

```
docker pull sequenceiq/hadoop-docker:2.7.1
```

# Start a container

In order to use the Docker image you have just build or pulled use:

**Make sure that SELinux is disabled on the host. If you are using boot2docker you don't need to do anything.**

```
docker run -it sequenceiq/hadoop-docker:2.7.1 /etc/bootstrap.sh -bash
```

## Testing

You can run one of the stock examples:

```
cd $HADOOP_PREFIX
# run the mapreduce
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.1.jar grep input output 'dfs[a-z.]+'

# check the output
bin/hdfs dfs -cat output/*
```

## Hadoop native libraries, build, Bintray, etc

The Hadoop build process is no easy task - requires lots of libraries and their right version, protobuf, etc and takes some time - we have simplified all these, made the build and released a 64b version of Hadoop nativelibs on this [Bintray repo](https://bintray.com/sequenceiq/sequenceiq-bin/hadoop-native-64bit/2.7.0/view/files). Enjoy.

## Automate everything

As we have mentioned previousely, a Docker file was created and released in the official [Docker repository](https://registry.hub.docker.com/u/sequenceiq/hadoop-docker/)
