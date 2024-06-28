FROM debian:bookworm-slim AS base
ENV USER="dev"
ENV GROUP="dev"
ENV HOME="/home/$USER"

RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "apt-transport-https", "curl", "git", "sudo", "zsh"]
RUN ["mkdir", "/workspace"]

RUN addgroup $GROUP \
    && useradd -mg $USER -G sudo -s /usr/bin/zsh $USER \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

FROM base AS utilities

RUN ["apt-get", "install", "-y", "nano"]

FROM base AS shell
USER dev

RUN sh -c "$(curl -fsSL https://install.ohmyz.sh)" \
    && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $HOME/.oh-my-zsh/custom/themes/powerlevel10k
COPY .zshrc .p10k.zsh $HOME
