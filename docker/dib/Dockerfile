FROM centos:7
MAINTAINER Chris Hoge (chris@openstack.org)
RUN yum update -y
RUN yum install -y epel-release
RUN yum install -y git python3 python-pip which qemu-img sudo e2fsprogs
RUN yum clean all
RUN git clone https://github.com/openstack/diskimage-builder.git
RUN cd /diskimage-builder \
&& pip3 install --upgrade pip \
&& pip3 install -r requirements.txt \
&& pip3 install .
ENTRYPOINT ["/bin/bash"]
