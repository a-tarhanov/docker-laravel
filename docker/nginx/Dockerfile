FROM nginx:alpine

RUN apk update \
    && apk upgrade \
    && apk add --no-cache openssl \
    && apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data

COPY nginx.conf /etc/nginx/
COPY app.template /etc/nginx/conf.d/

ARG SERVER_NAME
ENV SERVER_NAME ${SERVER_NAME}
RUN envsubst '\$SERVER_NAME' < /etc/nginx/conf.d/app.template > /etc/nginx/conf.d/default.conf

ADD ./startup.sh /opt/startup.sh
RUN sed -i 's/\r//g' /opt/startup.sh
CMD ["/bin/bash", "/opt/startup.sh"]

EXPOSE 80 443
