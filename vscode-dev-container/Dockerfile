FROM alpine:latest
    # Description of packages:
    #  - bash: Install bash cli interface
    #  - tzdata: To be able to change the timezone
    #  - gcompat: Provides compatibility with Glibc needed for Openshift Client (OC)
    #  - openrc: Provices rc-update command for configuring Docker
    #  - curl: For downloading the binaries of oc (Openshift) command
    #  - net-tools: Includes: arp, hostname, ifconfig, netstat, rarp, route, plipconfig, slattach, mii-tool and iptunnel and ipmaddr
    #  - python3 and py3-pip: For run DevOps scripts and dependencies
    #  - git: For clone remote repositories
    #  - helm: For deploy Helm packages in Kubernetes
    #  - openjdk11: Java OpenJDK required by Kafka command line tools
    #  - redis: Command line tools for Redis
    #  - docker and docker-cli-buildx: To be able to build new docker images
    RUN apk add --update --virtual .devops-tools --no-cache bash tzdata gcompat openrc curl net-tools python3 py3-pip git helm openjdk11 redis docker docker-cli-buildx

    # Switch to bash
    RUN bash

    # Change timezone
    ENV TZ=Europe/Madrid
    RUN cp /usr/share/zoneinfo/Europe/Madrid /etc/localtime

    # Configure Docker
    RUN addgroup root docker && rc-update add docker default

    # Install Openshift OC command
    RUN curl -L https://mirror.openshift.com/pub/openshift-v4/clients/oc/latest/linux/oc.tar.gz | tar xzvf - -C /usr/bin

    # Redirect kubectl command to oc
    RUN echo 'alias kubectl="oc"' >> ~/.bashrc && source ~/.bashrc

    # Install Homebrew, required by Terraform
    #RUN curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh

    # Install Terraform
    #RUN brew tap hashicorp/tap && brew install hashicorp/tap/terraform

    # Install MongoDB command line client
    #RUN brew install mongocli

    # Install Kafka command line tools
    RUN curl -L https://downloads.apache.org/kafka/3.7.0/kafka_2.13-3.7.0.tgz | tar xzvf - -C $HOME

    # Install VS CLI "code" command
    RUN curl -L 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' | tar xzvf - -C /usr/bin

    # Run VSCode
    ENTRYPOINT [ "code", "tunnel"]

    # Keep container alive
    #ENTRYPOINT [ "tail", "-f", "/dev/null" ]
