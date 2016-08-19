# "ported" by Adam Miller <maxamillion@fedoraproject.org> from
#   https://github.com/fedora-cloud/Fedora-Dockerfiles
#
# Originally written for Fedora-Dockerfiles by
#   scollier <scollier@redhat.com>

FROM centos:centos7
MAINTAINER The CentOS Project <cloud-ops@centos.org>

RUN yum -y update; yum clean all
RUN yum -y install openssh-server openssh-clients passwd; yum clean all
ADD ./id_rsa.pub /id_rsa.pub
RUN mkdir -p /root/.ssh
RUN cat /id_rsa.pub > /root/.ssh/authorized_keys
RUN chmod 644 /root/.ssh/authorized_keys
RUN echo -e "123456\n123456" | (passwd --stdin root)

ADD ./start.sh /start.sh
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

# RUN chmod 755 /start.sh
# EXPOSE 22
# RUN ./start.sh
ENTRYPOINT ["/usr/sbin/sshd", "-D"]
