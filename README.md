### hdp-2-Ambari-and-HDP-local-repository

> Setting Up a Local Repository

```sh
# log as root
sudo su - root

# install packages
yum -y install wget 

# install yum utilities
yum install -y yum-utils createrepo

# create an HTTP server
yum clean all
yum -y update
yum -y install httpd
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --permanent --add-port=443/tcp
firewall-cmd --reload
systemctl enable httpd
systemctl start httpd
systemctl enable httpd
systemctl status httpd

# change permission
/usr/share/doc/httpd-2.4.6/httpd-vhosts.conf

# create a directory for your web server
mkdir -p /var/www/html/

# create hdf repo folder
mkdir /var/www/html/repo
chmod 755 /var/www/html/repo

# get ambari tarball (https://docs.hortonworks.com/HDPDocuments/Ambari-2.5.1.0/bk_ambari-installation/content/ambari_repositories.html)
wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.5.1.0/ambari-2.5.1.0-centos7.tar.gz
wget http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.5.1.0/ambari.repo

# get hdp tarball (https://docs.hortonworks.com/HDPDocuments/Ambari-2.5.1.0/bk_ambari-installation/content/hdp_stack_repositories.html)
wget http://public-repo-1.hortonworks.com/HDP/centos7/2.x/updates/2.5.6.0/HDP-2.5.6.0-centos7-rpm.tar.gz
wget http://public-repo-1.hortonworks.com/HDP-UTILS-1.1.0.21/repos/centos7/HDP-UTILS-1.1.0.21-centos7.tar.gz
wget http://public-repo-1.hortonworks.com/HDP/centos7/2.x/updates/2.5.6.0/hdp.repo

# check files
cat *.repo

# untar file
mkdir HDP-UTILS
tar -xvzf ambari-2.5.1.0-centos7.tar.gz; tar -xvzf HDP-2.5.6.0-centos7-rpm.tar.gz; tar -xvzf HDP-UTILS-1.1.0.21-centos7.tar.gz -C HDP-UTILS

# copy file into repo folder
mkdir /var/www/html/repo/AMBARI
mkdir /var/www/html/repo/HDP
mkdir /var/www/html/repo/HDP-UTILS

chmod 755 /var/www/html/repo/AMBARI
chmod 755 /var/www/html/repo/HDP
chmod 755 /var/www/html/repo/HDP-UTILS

cp -r ambari/* /var/www/html/repo/AMBARI/
cp -r  HDP/* /var/www/html/repo/HDP/
cp -r HDP-UTILS/* /var/www/html/repo/HDP-UTILS/

# check files
ll /var/www/html/repo

```


> Go to go to http://IP/repo/ or http://hostname/repo

You should see something like this

> Set ambari repo
```sh
cat ambari.repo

vi ambari.repo

baseurl=http://velvet-repos.c.equipe-1314.internal/repo/AMBARI/centos7
gpgkey=http://velvet-repos.c.equipe-1314.internal/repo/AMBARI/centos7/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins

```

> Set hdp repo
```sh
cat hdp.repo

vi hdp.repo

baseurl=http://velvet-repos.c.equipe-1314.internal/repo/HDP/centos7/
gpgkey=http://velvet-repos.c.equipe-1314.internal/repo/HDP/centos7/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins

baseurl=http://velvet-repos.c.equipe-1314.internal/repo/HDP-UTILS/
gpgkey=http://velvet-repos.c.equipe-1314.internal/repo/HDP-UTILS/RPM-GPG-KEY/RPM-GPG-KEY-Jenkins

```

> copy repo file 
```sh
cp ambari.repo ambari.repo.bpk
cp hdp.repo hdp.repo.bpk

cp ambari.repo /var/www/html/repo/AMBARI/centos7/
cp hdp.repo /var/www/html/repo/HDP/centos7/

```
