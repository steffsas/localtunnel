FROM nginx:latest

# install openssh-server and sudo
RUN apt update && apt install openssh-server sudo -y

# add user development with home directory /home/development
# add user development to sudoers group 
RUN useradd -rm -d /home/development -s /bin/bash -g root -G sudo -u 1000 development

#RUN echo 'development:development' | chpasswd

# create directory for ssh keys
RUN mkdir /home/development/.ssh/ 

WORKDIR /home/development/.ssh/

# copy public key to ssh folder of development
COPY id_rsa.pub ./

# add public key to authorized keys
RUN cat id_rsa.pub >> authorized_keys

# change chmod for security reasons
RUN chmod 600 authorized_keys

# change directory owner
RUN chown development:root . -R

WORKDIR /

# enable public key auth
#RUN echo 'PubkeyAuthentication yes\nAuthorizedKeysFile .ssh/authorized_keys' >> /etc/ssh/sshd_config

RUN service ssh start

COPY entrypoint.sh entrypoint.sh

RUN chmod +x entrypoint.sh

CMD ["./entrypoint.sh"]
