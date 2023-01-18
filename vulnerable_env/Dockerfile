FROM debian:latest

ENV COMMIT cb6d43a677c338db930bc4e9161620832c1ec624

RUN apt-get -y -q update; \
    apt-get -y -q install xxd git unzip wget nano python3 python3-pip build-essential libffi-dev openssl rustc libssl-dev

RUN mkdir -p /opt/tools/ \
    && cd /opt/tools/ \
    && git clone https://github.com/fortra/impacket/ \
    && cd impacket \
    && git reset --hard ${COMMIT}

RUN cd /opt/tools/impacket/ \
    && python3 -m pip install -r requirements.txt \
    && python3 -m pip install .

RUN echo "#!/bin/bash" > /entrypoint.sh ;\
    echo "mkdir -p /share/" >> /entrypoint.sh ;\
    echo "echo 'Test file' > /share/test.txt" >> /entrypoint.sh ;\
    echo "python3 /opt/tools/impacket/examples/smbserver.py -smb2support SYSVOL /share/" >> /entrypoint.sh ;\
    chmod +x /entrypoint.sh

EXPOSE 445

CMD /entrypoint.sh
