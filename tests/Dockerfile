FROM ubuntu:23.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
    python3-pip

RUN pip3 install pytest pytest-testinfra ansible --break-system-packages && mkdir -p /conjurinc/

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
RUN apt-get update && \
    apt-get install -y docker-ce && \
    apt-get install -y gcc build-essential

RUN apt update && \
    apt install -y ruby-full
RUN gem install conjur-cli

WORKDIR /conjurinc/

CMD ["/bin/sleep", "1d"]
