# Dockerfile for clamav service
FROM alpine:3.13
# python3 shared with most images
RUN apk add --no-cache \
    python3 py3-pip \
  && pip3 install --upgrade pip
# Image specific layers under this line
RUN apk update && apk add pv clamav=0.103.2-r0 clamav-libunrar unrar && apk add --upgrade openssl && apk add --no-cache ca-certificates

ARG START_CON
ARG HEALTH_CON
ARG SCAN_CON
ARG CONF_CON

ADD ${CONF_CON} /etc/clamav-custom
ADD ${START_CON} /start.py
ADD ${HEALTH_CON} /health.sh
ADD ${SCAN_CON} /scan.sh
RUN chmod +x /health.sh /scan.sh

CMD ["python3", "/start.py"]
