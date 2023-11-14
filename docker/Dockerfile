FROM fedora:39

RUN dnf install -y virt-manager openssh-clients openssh-askpass dbus-x11  && \
    dnf upgrade -y && \
    dnf clean all

ENV DISPLAY="host.docker.internal:0"
ENV SSH_AUTH_SOCK="/run/host-services/ssh-auth.sock"

COPY /root /

# Create application user
RUN useradd -u 1001 -r -g 0 -d /home/default -s /sbin/nologin \
        -c "Default Application User" default && \
    chmod 700 /home/default/.ssh/ && chmod 600 /home/default/.ssh/* && \
    chown -R 1001:0 /home/default && chmod 755 /usr/bin/run-container

# Prepare DBUS
RUN dbus-uuidgen > /var/lib/dbus/machine-id && \
    mkdir -p /var/run/dbus

VOLUME ["/home/default/.config"]

CMD "/usr/bin/run-container"