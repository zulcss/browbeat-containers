FROM centos:7

RUN yum update -y && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y gcc gcc-c++ python2-devel python2-pip sudo git sudo && \
    pip install -U pip setuptools && \
    useradd -u 65500 -m rally && \ 
    usermod -aG wheel rally && \
    echo "rally ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/00-rally-user

RUN pip install --ignore-installed -U ipaddress && \
    pip install rally rally-openstack && \
    mkdir -p /etc/rally /var/lib/rally/data && \
    echo "[database]" > /etc/rally/rally.conf && \
    echo "connection=sqlite:////home/rally/data/rally.db" >> /etc/rally/rally.conf

USER rally
ENV HOME /home/rally
RUN mkdir -p /home/rally/data && rally db recreate

VOLUME  ["/home/rally/data"]
ENTRYPOINT ["rally"]
