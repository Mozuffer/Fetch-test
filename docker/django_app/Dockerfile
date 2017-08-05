FROM centos:7

# Install EPEL
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install python-django -y 

COPY djangoapp.tar.gz /
RUN tar -zxvf /djangoapp.tar.gz
 
EXPOSE 8080

CMD ["python","/djangoapp/manage.py","runserver","0.0.0.0:8080"]


