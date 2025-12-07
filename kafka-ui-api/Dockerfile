#FROM azul/zulu-openjdk-alpine:17-jre-headless
FROM azul/zulu-openjdk-alpine@sha256:2c13b82cc02e4e9573e94274abba8407010b74dcd11090dc48b3bb4af9aefc87

RUN apk add --no-cache \
    # snappy codec
    gcompat \
    # configuring timezones
    tzdata
RUN addgroup -S kafkaui && adduser -S kafkaui -G kafkaui

# creating folder for dynamic config usage (certificates uploads, etc)
RUN mkdir /etc/kafkaui/
RUN chown kafkaui /etc/kafkaui

USER kafkaui

ARG JAR_FILE
COPY "/target/${JAR_FILE}" "/kafka-ui-api.jar"

ENV JAVA_OPTS=

EXPOSE 8080

# see JmxSslSocketFactory docs to understand why add-opens is needed
CMD java --add-opens java.rmi/javax.rmi.ssl=ALL-UNNAMED  $JAVA_OPTS -jar kafka-ui-api.jar
