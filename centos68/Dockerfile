FROM centos:6.8

MAINTAINER XT-SERVER

RUN yum install -y wget curl telnet vim sudo crontabs ntp tcpdump iptables man zip unzip bzip2 tar git && \

rm -rf /var/lib/yum/history/* && rpm --import /etc/pki/rpm-gpg/RPM* && \
cd /etc/yum.repos.d && mv CentOS-Base.repo CentOS-Base.repo.backup && \
wget http://mirrors.163.com/.help/CentOS6-Base-163.repo && mv CentOS6-Base-163.repo CentOS-Base.repo && \
rpm -Uvh http://ftp.sjtu.edu.cn/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm && \

yum install -y sysstat gdb gcc gcc-c++ gcc-gfortran make cmake autoconf automake libtool libtool-libs glibc glibc-devel openssl openssl-devel zlib zlib-devel pcre pcre-devel gd gd-devel libiconv libmcrypt libmcrypt-devel mcrypt libcurl libcurl-devel libpng libpng-devel libjpeg libjpeg-devel libevent libevent-devel mlocate libxslt libxml2 libxml2-devel libxslt-devel libicu-devel bzip2-devel sqlite-devel rsync && \
updatedb && \

yum clean all && rm -rf /var/cache/yum/*

RUN rm -f /etc/localtime && \
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
ntpdate cn.pool.ntp.org

RUN groupadd www-data && \
useradd -g www-data www-data -s /sbin/nologin && \
usermod -u 1000 www-data && usermod -G ftp www-data && \
mkdir /data/ /data/app/ /data/www/ /data/static/ /data/sh/ /data/etc/ /data/log/ && \
chown -R www-data:www-data /data/www/ /data/static/ && \
echo -e "*/1 * * * * chown -R www-data:www-data /data/www/ /data/static/;" >> /var/spool/cron/root && \
echo -e "*/10 * * * * /usr/sbin/ntpdate cn.pool.ntp.org" >> /var/spool/cron/root && \
/etc/rc.d/init.d/crond start

RUN cd ~ && \
export TERM=xterm-256color && \
export LANG="en_US.UTF-8" && \
echo -e 'LANG="en_US.UTF-8"\nSYSFONT="latarcyrheb-sun16"' >> /etc/sysconfig/i18n && \
source /etc/sysconfig/i18n && \

echo -e "\nset nu\nset t_Co=256" >> /etc/vimrc && \

echo -e "\n\
alias vi='vim' \n\
alias ll='ls -al' \n\
alias la='ls -a' \n\
alias lw='ls -al | wc -l' \n\
\n\
alias ..='cd ..' \n\
\n\
alias findd='find -type d -name' \n\
alias findf='find -type f -name' \n\
\n\
alias grep='grep --color=auto' \n\
alias cmount='mount | column -t' \n\
alias meminfo='free -m -l -t' \n\
\n\
alias gz='tar -zxvf' \n\
\n\
export TERM=xterm-256color" >> ~/.bashrc && \

source ~/.bashrc && \

echo 'unset MAILCHECK' >> /etc/profile && source /etc/profile

CMD ["tail", "-f", "/dev/null"]