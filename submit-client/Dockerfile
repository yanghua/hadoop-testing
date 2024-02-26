# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG PROJECT_VERSION
FROM hadoop-testing/base-ubuntu-2204:$PROJECT_VERSION

ARG HADOOP_VERSION
ARG SPARK_VERSION
ARG KYUUBI_VERSION

ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CONF_DIR=/etc/hadoop/conf
ENV HADOOP_CLASSPATH=${HADOOP_HOME}/share/hadoop/client/*
ENV SPARK_HOME=/opt/spark
ENV SPARK_CONF_DIR=/etc/spark/conf
ENV KYUUBI_HOME=/opt/kyuubi
ENV KYUUBI_CONF_DIR=/etc/kyuubi/conf
ENV PATH=${KYUUBI_HOME}/bin:${SPARK_HOME}/bin:${HADOOP_HOME}/bin:${PATH}

ADD download/hadoop-${HADOOP_VERSION}.tar.gz /opt
ADD download/spark-${SPARK_VERSION}-bin-hadoop3.tgz /opt
ADD download/apache-kyuubi-${KYUUBI_VERSION}-bin.tgz /opt

# Copy configuration files
COPY ./files /

RUN ln -snf /opt/hadoop-${HADOOP_VERSION} ${HADOOP_HOME} && \
    ln -snf /opt/apache-kyuubi-${KYUUBI_VERSION}-bin ${KYUUBI_HOME} && \
    ln -snf spark-${SPARK_VERSION}-bin-hadoop3 /opt/spark

RUN chown -R hadoop:hadoop /opt/hadoop-${HADOOP_VERSION} && \
    chown -R kyuubi:hadoop /opt/apache-kyuubi-${KYUUBI_VERSION}-bin && \
    chown -R spark:hadoop /opt/spark-${SPARK_VERSION}-bin-hadoop3

CMD supervisord -c /etc/supervisord.conf
