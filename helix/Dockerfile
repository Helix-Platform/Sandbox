FROM python:2.7

MAINTAINER Fabio H. Cabrini "fabio.cabrini@gethelix.org"

WORKDIR /helix

COPY . .

RUN curl -sSL https://get.docker.com | sh

RUN pip install --upgrade pip

RUN pip install -r requirements.txt

CMD ["python","run.py"]
