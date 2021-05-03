FROM centos:centos8
ENV http_proxy='http://10.118.0.48:3128'
ENV https_proxy='http://10.118.0.48:3128'
USER root
RUN yum update -y
RUN dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --add-repo https://download.opensuse.org/repositories/Virtualization:/Appliances:/Builder/CentOS_8/
RUN rpm --import https://build.opensuse.org/projects/Virtualization:Appliances:Builder/public_key
RUN yum install -y \
	python36-devel.x86_64 \ 
	gcc 
RUN pip3 install kiwi
RUN yum -y  install \
	createrepo \
	rsync \ 
	qemu-img \
	gdisk \
	parted \
	xfsprogs
RUN mkdir -p /root/kiwi-descriptions/samples
RUN mkdir /root/local_repositories
COPY config.xml /root/kiwi-descriptions/samples
COPY config.sh /root/kiwi-descriptions/samples
