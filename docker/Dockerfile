ARG BASE_IMAGE=crs4/hadoopclient:3.2.0
FROM $BASE_IMAGE


ARG NB_USER=jovyan
ARG NB_UID=1000
ENV USER ${NB_USER}
ENV NB_UID ${NB_UID}
ENV HOME /home/${NB_USER}

# Make sure the contents of our repo are in ${HOME}
COPY . ${HOME}
USER root
RUN chown -R ${NB_UID} ${HOME}
USER ${NB_USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${NB_UID} \
    ${NB_USER}


ENV HADOOP_HOME /opt/hadoop
RUN apt update && \
    apt install -y  python3-pip && \
    pip3 install tiledb

RUN echo "export CLASSPATH=`$HADOOP_HOME/bin/hadoop classpath --glob`" >>  /etc/bash.bashrc && \
    echo "source /etc/profile.d/hadoop.sh" >> /etc/bash.bashrc
