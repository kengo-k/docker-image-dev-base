FROM ubuntu:22.04

LABEL org.opencontainers.image.description="開発環境用のイメージのためのベースとなるイメージです。"

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# install required packages
RUN apt-get update && \
  apt-get install -y \
    curl \
    zsh \
    git \ 
    openssh-client \
    build-essential

# setup user
ARG USERNAME=container-user
ARG USER_UID=3000
ARG USER_GID=$USER_UID
RUN groupadd -r -g $USER_GID $USERNAME && useradd -r -u $USER_UID -g $USERNAME -m -s /bin/zsh $USERNAME

USER $USERNAME
SHELL ["/bin/zsh", "-c"]

# install oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

COPY .zshrc /home/container-user/.zshrc

# install asdf
RUN git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.11.2

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/bin/zsh"]