# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM gcr.io/fuzzbench/base-image

ENV WORK /work
WORKDIR $WORK

# Install runtime dependencies for benchmarks, easy json parsing.
RUN apt-get update -y && apt-get install -y \
    jq \
    libglib2.0-0 \
    libxml2 \
    libarchive13 \
    libgss3

RUN virtualenv --python=$(which python3) $WORK/.venv

# Install docker cli.
RUN DOCKER_VERSION=18.09.7 && \
    curl -O https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz && \
    tar -xvzf docker-$DOCKER_VERSION.tgz && \
    mv docker/docker /usr/bin/ && \
    rm -rf docker docker-$DOCKER_VERSION.tgz

# Install cloud sql proxy.
RUN curl https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 > \
    /usr/local/bin/cloud_sql_proxy
RUN chmod +x /usr/local/bin/cloud_sql_proxy

COPY startup-dispatcher.sh $WORK/
