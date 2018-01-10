# dockerfile for Pulse tool deployment. © Author

FROM python:2.7
LABEL author="Vikash Bajaj"

ENV PYTHONIOENCODING=utf-8

RUN apt update
RUN apt install -y nginx supervisor
RUN pip install gunicorn
RUN pip install setuptools


# Build folder
RUN mkdir -p /deploy/app
WORKDIR /deploy/app
COPY ./requirements.txt /deploy/app/requirements.txt

# install dependencies
RUN pip install -r /deploy/app/requirements.txt

# Setup nginx
RUN rm /etc/nginx/sites-enabled/default
COPY deployment_configs/nginx.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/nginx.conf /etc/nginx/sites-enabled/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Setup supervisord
RUN mkdir -p /var/log/supervisor
COPY deployment_configs/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY deployment_configs/{{cookiecutter.repo_name}}_supervisor.conf /etc/supervisor/conf.d/

#Start sh
CMD ["/bin/bash"]
