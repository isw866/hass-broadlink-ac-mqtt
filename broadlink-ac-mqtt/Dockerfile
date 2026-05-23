ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

RUN apk add --no-cache gcc g++ make \
    && pip3 install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    pycryptodome~=3.23.0 \
    && cd /usr/share \
    && wget -c https://github.com/Arbuzov/broadlink_ac_mqtt/archive/refs/tags/1.2.2.tar.gz -O - | tar -xz \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/*
