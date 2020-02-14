ARG ELASTIC_SEARCH_VERSION

FROM docker.elastic.co/elasticsearch/elasticsearch:${ELASTIC_SEARCH_VERSION}

RUN elasticsearch-plugin install repository-s3 --batch
