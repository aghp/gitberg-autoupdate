FROM python:3

EXPOSE 80

RUN apt-get update && apt-get -y install cron logrotate && apt-get clean

RUN mkdir /var/log/gitenberg
COPY deploy/logrotate-gitberg-autoupdate /etc/logrotate.d/

WORKDIR /usr/src/app

# This is slow, so avoid having to do it every time.
RUN pip install boto3 travispy github3.py requests GitPython
COPY . .
RUN pip install .

CMD service cron start && exec webhook_server --port 80 --log_file /var/log/gitenberg/webhook_server
