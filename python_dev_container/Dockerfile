FROM python:3.12 AS builder

WORKDIR /home

ARG VENV_PATH_BUILDER="/opt/venv"

RUN python -m venv ${VENV_PATH_BUILDER}
ENV PATH="${VENV_PATH_BUILDER}/bin:$PATH"

# COPY requirements.txt .
# RUN pip install --upgrade pip \
#  && pip install --no-cache-dir -r requirements.txt


# ========================================


FROM python:3.12-slim AS dev

ARG UID=1000 # 整数型で渡す
ARG USER_NAME="keisuke"

ARG GID=1000 # 整数型で渡す
ARG GROUP_NAME="keisuke"

ARG VENV_PATH_DEV="/opt/venv"
ARG VENV_PATH_BUILDER="/opt/venv"

WORKDIR /home

RUN apt-get update \
 && apt-get install -y \
    vim \
    curl \
 && groupadd --gid ${GID} ${GROUP_NAME} \
 && useradd --create-home --uid ${UID} --gid ${GID} --shell /bin/bash ${USER_NAME} \
 && rm -rf /var/lib/apt/lists/*

COPY --from=builder --chown=${USER_NAME}:${GROUP_NAME} ${VENV_PATH_BUILDER} ${VENV_PATH_DEV}
ENV PATH="${VENV_PATH_DEV}/bin:$PATH"
USER ${USER_NAME}