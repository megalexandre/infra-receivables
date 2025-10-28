FROM ruby:3.4.7-bookworm

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    RBENV_ROOT=/usr/local/rbenv \
    PATH=/usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends locales && \
    sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen && \
    apt-get install -y \
    build-essential \
    libpq-dev \
    postgresql-client \
    git \
    curl \
    vim \
    nano \
    wget \
    sudo && \
    rm -rf /var/lib/apt/lists/*

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash \
    && echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN gem install \
    bundler \
    rails \
    pg \
    puma \
    debug \
    rdbg

ENV BUNDLE_PATH=/usr/local/bundle

RUN mkdir -p /workspace && chown -R $USERNAME:$USERNAME /workspace
WORKDIR /workspace

USER $USERNAME
