FROM python:3.12.12-slim

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    UV_SYSTEM_PYTHON=1

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    git \
    curl \
    wget \
    build-essential \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Create non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Switch to non-root user
USER $USERNAME
ENV PATH="/home/$USERNAME/.local/bin:$PATH"

# Install uv (modern Python package installer)
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Install ruff (Python linter and formatter) globally
RUN /home/vscode/.local/bin/uv tool install ruff

# Create workspace directory
WORKDIR /workspace

# Expose Jupyter port
EXPOSE 8888

CMD ["/bin/bash"]