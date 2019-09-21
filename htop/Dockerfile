# htop in a container
#
# docker run --rm -it \
# 	--pid host \
# 	jess/htop
#
FROM alpine:latest
LABEL maintainer "m0wer <m0wer@autistici.org>"

RUN apk --no-cache add \
	htop

CMD [ "htop" ]
