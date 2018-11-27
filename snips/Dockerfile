ARG BUILD_FROM
FROM $BUILD_FROM

# Copy data
COPY run.sh /
COPY mosquitto.conf /etc/
COPY customtts.sh /usr/bin

RUN chmod a+x /run.sh \
    && chmod a+x /usr/bin/customtts.sh \
    && apt-get update \
    && apt-get install -y mpg123 curl tzdata dirmngr \
    && bash -c  'echo "deb https://raspbian.snips.ai/$(lsb_release -cs) stable main" > /etc/apt/sources.list.d/snips.list' \
    && apt-key adv --keyserver pgp.mit.edu --recv-keys D4F50CDCA10A2849 \
    && apt-get update \
    && apt-get install -y snips-platform-voice snips-asr-injection || true \
    && rm -rf /var/lib/apt/lists/* \
    && curl -L -o /assistant_Hass_de.zip https://s3.amazonaws.com/hassio-addons-data/assistant_Hass_de.zip \
    && curl -L -o /assistant_Hass_en.zip https://s3.amazonaws.com/hassio-addons-data/assistant_Hass_en.zip \
    && curl -L -o /assistant_Hass_fr.zip https://s3.amazonaws.com/hassio-addons-data/assistant_Hass_fr.zip

ENTRYPOINT [ "/run.sh" ]
