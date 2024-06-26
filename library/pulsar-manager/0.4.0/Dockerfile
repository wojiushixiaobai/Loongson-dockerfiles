#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
FROM cr.loongnix.cn/library/openjdk:8u352

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Apache Pulsar Manager" \
      org.label-schema.description="An Apache Pulsar Manager for management Pulsar clusters" \
      org.label-schema.url="https://github.com/apache/pulsar-manager" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/apache/pulsar-manager" \
      org.label-schema.vendor="Apache Software Foundation" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

RUN apt-get update

RUN apt-get install --yes nginx supervisor postgresql \
  && rm  -rf /tmp/* \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /run/nginx

WORKDIR /pulsar-manager

RUN wget https://github.com/Loongson-Cloud-Community/pulsar-manager/releases/download/0.4.0/pulsar-manager.tar

#COPY pulsar-manager.tar .

RUN tar -xf pulsar-manager.tar

RUN rm -r pulsar-manager.tar

COPY supervisord.conf /etc/

COPY supervisord-token.conf /etc/

COPY supervisord-private-key.conf /etc/

COPY supervisord-secret-key.conf /etc/

COPY supervisord-configuration-file.conf /etc/

COPY default.conf /etc/nginx/conf.d/

COPY startup.sh /pulsar-manager/

COPY init_db.sql /pulsar-manager/

COPY entrypoint.sh /pulsar-manager/

COPY dist /usr/share/nginx/html/

ENTRYPOINT [ "/pulsar-manager/entrypoint.sh" ]
