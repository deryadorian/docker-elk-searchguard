# https://github.com/elastic/elasticsearch-docker
FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.3

RUN elasticsearch-plugin install -b com.floragunn:search-guard-5:5.6.3-16
# Add your elasticsearch plugins setup here
# Example: RUN elasticsearch-plugin install analysis-icu

COPY ./config/elasticsearch.yml /usr/share/elasticsearch/config/

USER root

RUN chown elasticsearch:elasticsearch /usr/share/elasticsearch/config/elasticsearch.yml

COPY ./plugins/search-guard-5/tools/install_demo_configuration.sh /usr/share/elasticsearch/plugins/search-guard-5/tools/

RUN chown elasticsearch:elasticsearch /usr/share/elasticsearch/plugins/search-guard-5/tools/install_demo_configuration.sh

USER elasticsearch:elasticsearch

RUN /usr/share/elasticsearch/plugins/search-guard-5/tools/install_demo_configuration.sh -y

RUN chmod 755 /usr/share/elasticsearch/plugins/search-guard-5/tools/sgadmin.sh

ENV ES_JAVA_OPTS="-Djavax.net.ssl.keyStore=/usr/share/elasticsearch/config/keystore.jks -Djavax.net.ssl.keyStorePassword=changeit -Djavax.net.ssl.trustStore=/usr/share/elasticsearch/config/truststore.jks -Djavax.net.ssl.trustStorePassword=changeit"

#CMD /usr/share/elasticsearch/bin/elasticsearch; /usr/share/elasticsearch/plugins/search-guard-5/tools/sgadmin.sh
#CMD elasticsearch && /usr/share/elasticsearch/sgadmin_demo.sh