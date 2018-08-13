FROM centos:6.8

MAINTAINER liuhanpeng <liuhanpeng@bossien.com>

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
	&& echo 'Asia/Shanghai' >/etc/timezone

RUN rm -rf /etc/yum.repos.d/* \
	&& curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo \
	&& yum clean all && yum makecache && yum update -y
