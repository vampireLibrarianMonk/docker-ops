FROM ubuntu:18.04

ENV VS_CODE_VERSION=1.72.2
ENV DONT_PROMPT_WSL_INSTALL=No_Prompt_please
#ENV USER_NAME=vstester
#ENV VS_DIR=/home/vstester

RUN apt-get update && apt-get upgrade -y

RUN apt-get install wget -y

RUN apt-get install libglib2.0-0 libnss3 libatk1.0-0 libatk-bridge2.0-0 libcups2 libdrm2 libgtk-3-0 libgbm1 libasound2  -y

#RUN useradd -m ${USER_NAME}

#RUN groupadd -r ${USER_NAME} -f -g 1001 && \
# useradd -u 1001 -r -g ${USER_NAME} -m -d ${VS_DIR} -s /sbin/nologin \
# -c "VS Tester" nexus && \
# chown -R ${USER_NAME}:${USER_NAME} ${VS_DIR} && \
# chmod -R 755 ${VS_DIR}

#USER ${USER_NAME}

WORKDIR ${VS_DIR}

RUN wget -q -O ${VS_CODE_VERSION}.tar.gz https://update.code.visualstudio.com/${VS_CODE_VERSION}/linux-x64/stable

RUN tar -xf ${VS_CODE_VERSION}.tar.gz

RUN rm -f ${VS_CODE_VERSION}.tar.gz

#ENTRYPOINT [ "tail", "-f", "/dev/null" ]
CMD /VSCode-linux-x64/bin/code 
#ENTRYPOINT [ "/VSCode-linux-x64/bin/code"]
