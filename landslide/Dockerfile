FROM debian:jessie

RUN apt-get update && apt-get install -y\
	python\
	git\
	markdown\
	python-pip &&\
	apt-get clean
RUN pip install landslide jinja2 pygments

ADD slides /var/www/html
ADD themes /var/www/html/themes

WORKDIR /var/www/html

CMD ["landslide", "-t", "themes/default", "--copy-theme", "--relative", "npug.md"]
