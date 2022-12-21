FROM mcr.microsoft.com/devcontainers/go:0-1.17-bullseye

# install pip
RUN apt-get update && apt-get -y install python3-pip

# install pre-commit hook environments
COPY .pre-commit-config.yaml .
RUN pip install pre-commit==2.20.0 && git init . && pre-commit install-hooks && rm -rf .git

# install gitleaks
RUN wget https://github.com/zricethezav/gitleaks/releases/download/v8.15.2/gitleaks_8.15.2_linux_arm64.tar.gz && tar -xvkf gitleaks_8.15.2_linux_arm64.tar.gz -C /usr/local/bin 

# don't create .pyc files
ENV PYTHONDONTWRITEBYTECODE 1
# get more data to container terminal
ENV PYTHONUNBUFFERED 1

# install python dependencies in next layer image
# RUN pip install --upgrade pip
# RUN pip install --no-cache-dir -r requirements.txt