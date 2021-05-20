# Dockerfile for clamav service
FROM alpine:3.13
# python3 shared with most images
RUN apk add --no-cache \
    python3 py3-pip \
  && pip3 install --upgrade pip
# Image specific layers under this line
RUN apk add --no-cache clamav rsyslog wget clamav-libunrar
RUN mkdir -p /logs /data
RUN echo `date`: File created >> /logs/clamscan.log

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
