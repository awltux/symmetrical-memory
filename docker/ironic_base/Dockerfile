FROM centos:7
MAINTAINER Chris Hoge (chris@openstack.org)
RUN yum install -y git python3 epel-release python-pip vim | tee /var/log/dockerfile.run.log
RUN yum install -y python-devel openssl-devel python-pip mysql-devel libxml2-devel libxslt-devel postgresql-devel git git-review libffi-devel gettext ipmitool psmisc graphviz gcc libjpeg-turbo-devel | tee -a /var/log/dockerfile.run.log
RUN pip install wheel python-ironicclient pymysql pip tox virtualenv --upgrade | tee -a /var/log/dockerfile.run.log
RUN git clone https://github.com/openstack/ironic.git | tee -a /var/log/dockerfile.run.log
RUN cd /ironic | tee -a /var/log/dockerfile.run.log
RUN tox -edocs | tee -a /var/log/dockerfile.run.log
RUN tox -egenconfig | tee -a /var/log/dockerfile.run.log
RUN pip install -r requirements.txt  | tee -a /var/log/dockerfile.run.log
RUN pip install . | tee -a /var/log/dockerfile.run.log
RUN mkdir -p /etc/ironic | tee -a /var/log/dockerfile.run.log
RUN cp -r /ironic/etc/ironic/* /etc/ironic/ | tee -a /var/log/dockerfile.run.log
ADD /boot.ipxe /etc/ironic/boot.ipxe
ADD /ironic.conf.sh /ironic.conf.sh
