FROM don41382/rpi-python3-with-bluetooth

USER root

# Install dependencies
RUN apt-get -yqq update && \
    apt-get -yqq --no-install-recommends install curl gnupg git build-essential bluez bluetooth usbutils && \
    apt-get -yqq autoremove && \
    apt-get -yqq clean && \
    rm -rf /var/lib/apt/lists/* /var/cache/* /tmp/* /var/tmp/*

RUN curl -sL https://deb.nodesource.com/setup_8.x  | bash -
RUN apt-get -y install nodejs
RUN which node

RUN usermod -a -G bluetooth root && \
    setcap cap_net_raw+eip /usr/bin/node
	
RUN git clone https://github.com/espruino/EspruinoHub /var/espruinohub

WORKDIR /var/espruinohub

RUN npm install --unsafe-perm

#Run other commands for start BLE...
COPY run.sh /var/espruinohub/cmd.sh
RUN chmod +x /var/espruinohub/cmd.sh

CMD /var/espruinohub/cmd.sh