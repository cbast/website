FROM mcr.microsoft.com/devcontainers/python:0-3.11

RUN export DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -y install libcairo2 && \
    rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt && \
    rm /tmp/requirements.txt
