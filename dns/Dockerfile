FROM debian:jessie

RUN apt-get update && apt-get install -y\
	dnsmasq\
	dnsutils\
	&& apt-get clean

RUN echo >> /etc/dnsmasq.conf
RUN echo "addn-hosts=/etc/althosts" >> /etc/dnsmasq.conf
RUN echo "user=root" >> /etc/dnsmasq.conf

EXPOSE 53

CMD ["/usr/sbin/dnsmasq","-d"]
