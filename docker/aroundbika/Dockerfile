# Based on gmauro/debian-ansible
FROM gmauro/debian-ansible
MAINTAINER Gianmauro Cuccuru <gmauro@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

WORKDIR $(mktemp -d)
# cache buster: date | md5sum | cut -f 1 -d ' '
RUN git clone https://github.com/crs4/aroundBika # 343fb57c8016b5ad019e1aee24292249
RUN ansible-playbook -i localhost, aroundBika/aroundBika.yml

EXPOSE 8081

RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
ADD supervisord.conf /etc/supervisor/supervisord.conf

# Clean up any files used by apt-get
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]