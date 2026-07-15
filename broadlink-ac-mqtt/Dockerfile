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
    && python3 -c " \
file_path = '/usr/share/broadlink_ac_mqtt-1.2.3/broadlink_ac_mqtt/classes/broadlink/ac_db.py'; \
with open(file_path, 'r', encoding='utf-8') as f: content = f.read(); \
old_line = 'status_nice[\'fanspeed_homeassistant\']  = self.get_key(self.STATIC.FAN.__dict__,status[\'fanspeed\']).title()'; \
new_line = 'res_fan = self.get_key(self.STATIC.FAN.__dict__,status[\'fanspeed\'])\n        status_nice[\'fanspeed_homeassistant\'] = res_fan.title() if isinstance(res_fan, str) else str(res_fan)'; \
content = content.replace(old_line, new_line); \
with open(file_path, 'w', encoding='utf-8') as f: f.write(content); \
print('Successfully patched ac_db.py!')"
