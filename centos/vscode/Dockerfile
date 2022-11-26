# Use the following run command to get this thing working!
# docker run -d --net=host --name gui_test --privileged --env DISPLAY=$DISPLAY -v "${HOME}/Xauthority:/root/.Xauthority:rw" -v /tmp/.X11-unix:/tmp/.X11-unix centos_gui:latest

# Original template based off of
# https://linuxize.com/post/how-to-install-visual-studio-code-on-centos-7/

# We are going to use the Latest version of Centos
FROM  centos:centos7.9.2009

ENV VS_CODE_VERSION=1.72.2

# Fixed immediate close of window upon boot with: https://github.com/WhitewaterFoundry/Pengwin/issues/285
ENV LIBGL_ALWAYS_INDIRECT=1
ENV NO_AT_BRIDGE=1

# Installing the sources for the locales
RUN  yum install -y glibc-common wget

# Setting up the default locale to en_US.UTF-8
RUN  localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8 && \
     export LANG=en_US.UTF-8

# Installing Necessary packages including firefox
RUN  yum install -y dbus-x11 PackageKit-gtk3-module libcanberra-gtk2 firefox

# Generating a universally unique ID for the Container
RUN  dbus-uuidgen > /etc/machine-id

# Starting Firefox application
#CMD  /usr/bin/firefox

RUN wget -q -O ${VS_CODE_VERSION}.tar.gz https://update.code.visualstudio.com/${VS_CODE_VERSION}/linux-x64/stable

RUN tar -xf ${VS_CODE_VERSION}.tar.gz

RUN rm -f ${VS_CODE_VERSION}.tar.gz

RUN mkdir -p /home/vstester

RUN chmod +x /VSCode-linux-x64/bin/code

# Diagnostics 
#ENTRYPOINT ["tail", "-f", "/dev/null"]

#ENTRYPOINT ["./VSCode-linux-x64/bin/code", "--no-sandbox", "--user-data-dir", "/home/vstester" ]
CMD ./VSCode-linux-x64/bin/code --verbose --no-sandbox --user-data-dir /home/vstester
