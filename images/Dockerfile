FROM ubuntu:14.04

MAINTAINER Hocine Bendou <hocine@sanbi.ac.za>

RUN apt-get update && apt-get install -y \
        openssh-server \
        lsof \
        supervisor \
        build-essential \
        python-dev \
        git-core \
        libffi-dev \
        libpcre3-dev \
        gcc \
        autoconf \
        libtool \
        pkg-config \
        zlib1g-dev \
        libssl-dev \
        libexpat1-dev \
        libxslt1.1 \
        gnuplot \
        libpcre3 \
        libcairo2 \
        libpango1.0-0 \
        libgdk-pixbuf2.0-0 \
        libxml2-dev \
        libxslt-dev

ADD https://launchpad.net/plone/4.3/4.3.14/+download/Plone-4.3.14-UnifiedInstaller.tgz /opt/baobab/

RUN tar -xvf /opt/baobab/Plone-4.3.14-UnifiedInstaller.tgz -C /opt/baobab/

RUN sudo /opt/baobab/Plone-4.3.14-UnifiedInstaller/install.sh --target=/usr/local/Plone --password=secret --build-python zeo

RUN mkdir -p /var/local/Plone

COPY buildout.cfg /usr/local/Plone/zeocluster/buildout.cfg

RUN cd /usr/local/Plone/zeocluster && sudo -u plone_buildout bin/buildout

COPY ./baobab_supervisord.conf /etc/supervisor/conf.d/baobab.conf

RUN rm -rf /opt/baobab

EXPOSE 8080

CMD ["/usr/bin/supervisord"]
