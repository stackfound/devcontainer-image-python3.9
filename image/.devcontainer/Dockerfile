FROM mcr.microsoft.com/devcontainers/go:0-1.17-bullseye

# install preferred development tools
RUN apt-get update \
&& apt-get install -y fontconfig
RUN font_url='https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/FiraCode.zip'; font_name=${font_url##*/}; wget ${font_url} && unzip ${font_name} -d ~/.fonts && fc-cache -fv ;
RUN apt-get update \
&& sh -c "$(curl -fsSL https://starship.rs/install.sh)" -- -f \
&& apt-get install -y ne figlet nodejs npm \
&& chsh -s /usr/bin/fish

# install serverless framework
RUN yes | npm install -g serverless

# install gitname
RUN mkdir -p /usr/local/bin/gitname_install \
&& cd /usr/local/bin/gitname_install \
&& wget -O gitname.tar.gz https://github.com/alex-shpak/gitname/releases/download/v5/gitname_5_Linux_x86_64.tar.gz \
&& tar xzvf gitname.tar.gz --no-same-owner \
&& cp ./gitname /usr/local/bin \
&& rm -rf /usr/local/bin/gitname_install

# install pip
RUN apt-get update && apt-get -y install python3-pip

# install doppler cli
RUN apt-get update && apt-get install -y apt-transport-https ca-certificates curl gnupg \
&& curl -sLf --retry 3 --tlsv1.2 --proto "=https" 'https://packages.doppler.com/public/cli/gpg.DE2A7741A397C129.key' | apt-key add - \
&& echo "deb https://packages.doppler.com/public/cli/deb/debian any-version main" | tee /etc/apt/sources.list.d/doppler-cli.list \
&& apt-get update && apt-get install -y doppler

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