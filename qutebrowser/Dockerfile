FROM debian:stable-slim
MAINTAINER m0wer <m0wer@autistici.org>

RUN apt update && \
        apt install qutebrowser -y && \
        rm -rf /var/lib/apt/lists/*

RUN useradd -m qutebrowser
USER qutebrowser

CMD ["/usr/bin/qutebrowser"]
