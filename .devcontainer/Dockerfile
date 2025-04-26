FROM golang
WORKDIR /workspace

ARG USERNAME=devcontainer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# 依存関係のインストール
RUN apt update && apt upgrade -y && apt install -y sudo git gpg unzip

# ユーザーの作成
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME 

# protocのインストール
RUN curl -Lo protoc.zip "https://github.com/protocolbuffers/protobuf/releases/download/v30.2/protoc-30.2-linux-x86_64.zip"
RUN unzip -q ./protoc.zip bin/protoc "include/*" -d /usr/local
RUN chmod a+x /usr/local/bin/protoc
RUN rm -rf protoc.zip
