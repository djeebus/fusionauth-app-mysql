VERSION 0.6

ARG image_name="fusionauth-mysql"
ARG fusionauth_app_version=""
ARG mysql_connector_version="8.0.31"

download-connector:
    FROM alpine:3.15

    RUN FILE=mysql-connector-java.zip \
        URL=https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-j-${mysql_connector_version}.zip \
        && wget $URL --output-document $FILE \
        && unzip $FILE

    SAVE ARTIFACT ./mysql-connector-j-${mysql_connector_version}/mysql-connector-j-${mysql_connector_version}.jar mysql-connector-java-${mysql_connector_version}.jar

build-image:
    FROM fusionauth/fusionauth-app:${fusionauth_app_version}

    COPY +download-connector/mysql-connector-java-${mysql_connector_version}.jar /usr/local/fusionauth/fusionauth-app/lib/

    SAVE IMAGE --push ${image_name}:${fusionauth_app_version}
