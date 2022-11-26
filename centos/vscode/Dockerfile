# Use the following run command to get this thing working!
# docker run -d --net=host --name gui_test --privileged --env DISPLAY=$DISPLAY -v "${HOME}/Xauthority:/root/.Xauthority:rw" -v /tmp/.X11-unix:/tmp/.X11-unix centos_gui:latest

# While keeping the container running:
# docker exec -it gui_test ./home/vstester/VSCode-linux-x64/bin/code

# Original template based off of
# https://linuxize.com/post/how-to-install-visual-studio-code-on-centos-7/

# We are going to use the Latest version of Centos
FROM  centos:centos7.9.2009

# Create a user name
ENV USER_NAME=vstester
ENV VS_DIR=/home/${USER_NAME}

ENV VS_CODE_VERSION=1.72.2
ENV DEBUGGER_JAVA=0.46.2022112102
ENV EXTENSION_JAVA=0.25.2022110400
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk

# Fixed immediate close of window upon boot with: https://github.com/WhitewaterFoundry/Pengwin/issues/285
#ENV LIBGL_ALWAYS_INDIRECT=1
#ENV NO_AT_BRIDGE=1

# Installing the sources for the locales
RUN yum install -y glibc-common wget

# Setting up the default locale to en_US.UTF-8
RUN  localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8 && \
     export LANG=en_US.UTF-8

# Installing Necessary packages including firefox
RUN  yum install -y dbus-x11 PackageKit-gtk3-module libcanberra-gtk2 firefox

# Install SDK
RUN yum install -y java-11-openjdk-devel

# Generating a universally unique ID for the Container
RUN  dbus-uuidgen > /etc/machine-id

# Create directory structure
RUN mkdir -p ${VS_DIR}/VSCode-linux-x64 

# Download VSCode
RUN wget -q -O ${VS_DIR}/${VS_CODE_VERSION}.tar.gz https://update.code.visualstudio.com/${VS_CODE_VERSION}/linux-x64/stable 

RUN chmod +x+r ${VS_DIR}/${VS_CODE_VERSION}.tar.gz 

RUN tar -xf ${VS_DIR}/${VS_CODE_VERSION}.tar.gz  --directory ${VS_DIR}/ 

RUN rm -f ${VS_DIR}/${VS_CODE_VERSION}.tar.gz 

RUN useradd -m ${USER_NAME}

RUN groupadd -r ${USER_NAME} -f -g 1001 && \
 useradd -u 1001 -r -g ${USER_NAME} -m -d ${VS_DIR} -s /sbin/nologin \
 -c "VS Tester" nexus && \
 chown -R ${USER_NAME}:${USER_NAME} ${VS_DIR} && \
 chmod -R 755 ${VS_DIR}

USER ${USER_NAME}

# Install extension
RUN ./${VS_DIR}/VSCode-linux-x64/bin/code --install-extension vscjava.vscode-java-pack@${EXTENSION_JAVA}
RUN ./${VS_DIR}/VSCode-linux-x64/bin/code --install-extension vscjava.vscode-java-debug@${DEBUGGER_JAVA}

# Diagnostics 
ENTRYPOINT ["tail", "-f", "/dev/null"]

#ENTRYPOINT [ "./${VS_DIR}/VSCode-linux-x64/bin/code" ]
#CMD ./VSCode-linux-x64/bin/code --verbose --no-sandbox --user-data-dir /home/vstester
#CMD ${VS_DIR}/VSCode-linux-x64/bin/code
