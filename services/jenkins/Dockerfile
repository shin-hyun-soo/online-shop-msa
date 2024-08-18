FROM jenkins/jenkins:lts

USER root

# 시스템 업데이트 및 필요한 패키지 설치
RUN apt-get update && apt-get install -y \
    docker.io \
    curl \
    unzip

# AWS CLI 설치
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf aws awscliv2.zip

# Docker 그룹 생성 (이미 존재하지 않는 경우)
RUN groupadd -f docker

# Jenkins 사용자를 Docker 그룹에 추가
RUN usermod -aG docker jenkins

# Docker 소켓의 권한을 변경
RUN chmod 666 /var/run/docker.sock

# 작업 디렉토리 설정
WORKDIR /var/jenkins_home

# Jenkins 사용자로 전환
USER jenkins
