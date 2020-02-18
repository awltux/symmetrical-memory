FROM centos:7
MAINTAINER Chris Hoge (chris@openstack.org)
RUN yum erase -y git python-requests python-ipaddress
RUN yum install -y epel-release \
 && rpm -U https://centos7.iuscommunity.org/ius-release.rpm
RUN yum install -y git2u python3 python3-devel vim python-devel openssl-devel mysql-devel libxml2-devel libxslt-devel postgresql-devel libffi-devel gettext ipmitool psmisc graphviz gcc libjpeg-turbo-devel
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
 && python get-pip.py \
 && pip install --upgrade wheel python-ironicclient pymysql tox virtualenv
RUN git clone https://github.com/openstack/ironic.git \
 && cd /ironic \
 && tox -edocs \
 && tox -egenconfig \
 && pip install -r requirements.txt  \
 && pip install . \
 && mkdir -p /etc/ironic \
 && cp -r /ironic/etc/ironic/* /etc/ironic/
ADD /boot.ipxe /etc/ironic/boot.ipxe
ADD /ironic.conf.sh /ironic.conf.sh
