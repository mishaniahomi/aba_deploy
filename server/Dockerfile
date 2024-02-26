# Указывает Docker использовать официальный образ python 3 с dockerhub в качестве базового образа
FROM python:3.8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED 1
RUN mkdir /aba
WORKDIR /aba
COPY ./aba/requirements_ubuntu.txt /aba/
COPY ./aba/000-default.conf /aba/
COPY ./aba/redirect.conf /aba/
# Запускает команду pip install для всех библиотек, перечисленных в requirements_ubuntu.txt
RUN pip install --upgrade pip && pip install -r requirements_ubuntu.txt
RUN pip install django-haystack==2.4.0
RUN pip install pysolr==3.3.2
RUN apt-get update

RUN apt-get install -y apache2 nano libapache2-mod-wsgi-py3 

RUN rm /etc/apache2/sites-available/000-default.conf
RUN cp 000-default.conf /etc/apache2/sites-available/
RUN cp redirect.conf /etc/apache2/sites-available/

RUN mkdir -p /etc/httpd/ssl/
WORKDIR /etc/httpd/ssl
RUN openssl req -new -x509 -days 1461 -nodes -out cert.pem -keyout cert.key -subj "/C=RU/ST=SPb/L=SPb/O=Global Security/OU=IT Department/CN=test.dmosk.local/CN=test"
RUN a2enmod ssl
RUN a2ensite redirect.conf

WORKDIR /aba

# RUN python3 -m venv /.cp
# RUN /.cp/bin/pip install --no-cache-dir -r requirements_ubuntu.txt
