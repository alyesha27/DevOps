# Jenkins на основе официального образа + Ansible для плагина Ansible
FROM jenkins/jenkins:lts-jdk21

USER root

# Ansible нужен на самом Jenkins: плагин Ansible вызывает ansible-playbook.
# openssh-client — для подключения к удалённой ноде.
RUN apt-get update \
    && apt-get install -y --no-install-recommends python3 python3-pip python3-venv openssh-client \
    && rm -rf /var/lib/apt/lists/* \
    && python3 -m venv /opt/ansible-venv \
    && /opt/ansible-venv/bin/pip install --no-cache-dir ansible \
    && ln -s /opt/ansible-venv/bin/ansible* /usr/local/bin/

# Ansible требует UTF-8 локаль
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

USER jenkins

# Плагины: Ansible, цветной вывод, Pipeline, Git
RUN jenkins-plugin-cli --plugins ansible ansicolor workflow-aggregator git
