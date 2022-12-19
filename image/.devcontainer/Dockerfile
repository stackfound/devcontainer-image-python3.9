FROM mcr.microsoft.com/devcontainers/python:0-3.9-bullseye

# install gitleaks
RUN wget https://github.com/zricethezav/gitleaks/releases/download/v8.15.2/gitleaks_8.15.2_linux_arm64.tar.gz && tar -xvkf gitleaks_8.15.2_linux_arm64.tar.gz -C /usr/local/bin 

# don't create .pyc files
ENV PYTHONDONTWRITEBYTECODE 1
# get more data to container terminal
ENV PYTHONUNBUFFERED 1

# install python dependencies in next layer image
# RUN pip install --upgrade pip
# RUN pip install --no-cache-dir -r requirements.txt