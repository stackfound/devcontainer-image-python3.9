FROM golang:1.18-bullseye as base

# install pip
RUN apt-get update && apt-get -y install python3-pip

# install pre-commit hook environments
COPY .pre-commit-config.yaml .
RUN pip install pre-commit==2.20.0 && git init . && mkdir /pre-commit/ && PRE_COMMIT_HOME=/pre-commit/ pre-commit install-hooks && rm -rf .git

FROM mcr.microsoft.com/devcontainers/python:0-3.9-bullseye

COPY --from=base /pre-commit/ ~/.cache/pre-commit

# install pre-commit
RUN pip install pre-commit==2.20.0

# install gitleaks
RUN wget https://github.com/zricethezav/gitleaks/releases/download/v8.15.2/gitleaks_8.15.2_linux_arm64.tar.gz && tar -xvkf gitleaks_8.15.2_linux_arm64.tar.gz -C /usr/local/bin 

# don't create .pyc files
ENV PYTHONDONTWRITEBYTECODE 1
# get more data to container terminal
ENV PYTHONUNBUFFERED 1

# install python dependencies in next layer image
# RUN pip install --upgrade pip
# RUN pip install --no-cache-dir -r requirements.txt