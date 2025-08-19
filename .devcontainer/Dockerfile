FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

USER root

RUN apt-get update && apt-get install -y --no-install-recommends unzip curl \
    && ARCH_SUFFIX="" \
    && case "$(uname -m)" in \
    x86_64) ARCH_SUFFIX="amd64" ;; \
    aarch64) ARCH_SUFFIX="arm64" ;; \
    *) echo "Unsupported architecture: $(uname -m)" && exit 1 ;; \
    esac \
    && curl -sSL -o /usr/local/bin/tfsec "https://github.com/aquasecurity/tfsec/releases/latest/download/tfsec-linux-${ARCH_SUFFIX}" \
    && chmod +x /usr/local/bin/tfsec \
    && TD_VERSION=$(curl -s https://api.github.com/repos/terraform-linters/tflint/releases/latest | grep -oP '"tag_name": "\K(.*)(?=")') \
    && curl -sSL "https://github.com/terraform-docs/terraform-docs/releases/download/v${TD_VERSION}/terraform-docs-${TD_VERSION}-linux-${ARCH_SUFFIX}.tar.gz" | tar -xz -C /usr/local/bin/ \
    && curl -sSL -o /tmp/tflint.zip "https://github.com/terraform-linters/tflint/releases/latest/download/tflint_linux_${ARCH_SUFFIX}.zip" \
    && unzip /tmp/tflint.zip -d /usr/local/bin/ \
    && rm -rf /tmp/tflint.zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER vscode
