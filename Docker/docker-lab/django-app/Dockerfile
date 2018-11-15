FROM python:3
ENV PYTHONUNBUFFERED 1
ENV http_proxy=http://10.164.177.170:8080
ENV https_proxy=http://10.164.177.170:8080
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/