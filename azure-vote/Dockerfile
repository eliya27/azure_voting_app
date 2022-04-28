FROM tiangolo/uwsgi-nginx-flask:python3.6

WORKDIR /usr/src/app


RUN pip install redis

COPY . .


ADD /azure-vote/app

EXPOSE 8080
CMD ["start"]
