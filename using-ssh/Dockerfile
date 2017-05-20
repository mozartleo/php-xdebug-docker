FROM php:5.6-fpm
RUN pecl install xdebug-2.5.3 \
    && docker-php-ext-enable xdebug

COPY 99-xdebug.ini /usr/local/etc/php/conf.d/

RUN apt update && apt install -y openssh-server supervisor
RUN mkdir /var/run/sshd
RUN sed -i -e 's/PermitRootLogin without-password/PermitRootLogin yes/' -e '/AuthorizedKeysFile/s/^# *//' -e '/UsePrivilegeSeparation/s/yes/no/' /etc/ssh/sshd_config
RUN echo 'root:mypassword' | chpasswd

#RUN mkdir /root/.ssh && ssh-keygen -t rsa -P "" -C "SSH Client Key for XDebug" -f /root/.ssh/xdebug_client && cat /root/.ssh/xdebug_client.pub >> /root/.ssh/authorized_keys
COPY supervisor_app.conf /etc/supervisor/conf.d/
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
EXPOSE 80 443 22
CMD ["supervisord", "-n"]
