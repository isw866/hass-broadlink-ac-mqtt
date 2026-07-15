ARG BUILD_FROM
FROM $BUILD_FROM

COPY rootfs /

RUN apk add --no-cache gcc g++ make libffi-dev openssl-dev \
    && pip3 install --no-cache-dir -U \
    paho-mqtt \
    pyyaml \
    cryptography~=42.0 \
    && cd /usr/share \
    && wget -c https://github.com/Arbuzov/broadlink_ac_mqtt/archive/refs/tags/1.2.3.tar.gz -O - | tar -xz \
    && chmod a+x /etc/services.d/broadlink-ac-mqtt/* \
    && sed -i "s|status_nice\['fanspeed_homeassistant'\].*title()|res_fan = self.get_key(self.STATIC.FAN.__dict__,status['fanspeed']); status_nice['fanspeed_homeassistant'] = res_fan.title() if isinstance(res_fan, str) else str(res_fan)|" /usr/share/broadlink_ac_mqtt-1.2.3/broadlink_ac_mqtt/classes/broadlink/ac_db.py
