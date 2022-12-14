FROM python:3.10-slim-bullseye as poetry-base

RUN apt-get update && apt-get install -y curl

# https://python-poetry.org/docs/master/#installation
ENV POETRY_VERSION=1.2.0

RUN curl -sSL https://install.python-poetry.org | python3 - --version "$POETRY_VERSION"

# See "Add Poetry to your PATH" in https://python-poetry.org/docs/master/#installing-with-the-official-installer
ENV PATH="/root/.local/bin:$PATH"

FROM poetry-base

RUN apt-get update
# Used to check if postgress is running
RUN apt-get install -y netcat

# set work directory
WORKDIR /app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install dependencies
COPY ./pyproject.toml .
COPY ./poetry.lock .
RUN poetry config virtualenvs.create false
RUN poetry install

# copy project
COPY . .

# This allows for bind mounted code created in the container to be non root
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # Add sudo support
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set the default user
# USER $USERNAME

# run entrypoint.sh
ENTRYPOINT ["/app/entrypoint.sh"]