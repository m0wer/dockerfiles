FROM debian:stable-slim
MAINTAINER m0wer <m0wer@autistici.org>

RUN apt update && \
        apt install polar -y && \
        rm -rf /var/lib/apt/lists/*

RUN useradd -m polar
USER polar

CMD ["/usr/bin/qutebrowser"]
