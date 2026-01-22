FROM debian:bookworm-slim

# Install necessary dependencies
RUN apt update && apt install -y  \
    golang-go \
    wget \
    dos2unix \
    && apt clean

RUN wget https://go.dev/dl/go1.24.0.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.24.0.linux-amd64.tar.gz && \
    rm go1.24.0.linux-amd64.tar.gz

ENV PATH="/usr/local/go/bin:/root/go/bin:$PATH"

RUN go install github.com/mailhog/MailHog@latest

# Copy the commands directory into the container
COPY commands/setup_mailhog_auth.sh /commands/setup_mailhog_auth.sh

# Ensure all scripts in the commands directory have Unix-style line endings and are executable
RUN dos2unix /commands/setup_mailhog_auth.sh && chmod +x /commands/setup_mailhog_auth.sh

CMD ["MailHog"]
