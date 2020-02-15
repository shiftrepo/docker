FROM jenkins/jenkins:lts-alpine

USER root

ENV JENKINS_REF /usr/share/jenkins/ref

# install jenkins plugins
#COPY ./plugins.txt $JENKINS_REF/

RUN echo -e "\n\
git:latest\n\
junit:latest\n\
command-launcher:latest\n\
display-url-api:latest\n\
git-client:latest\n\
workflow-api:latest\n\
workflow-scm-step:latest\n\
workflow-step-api:latest\n\
timestamper:latest\n\
workflow-support:latest\n\
workflow-durable-task-step:latest\n\
matrix-project:latest\n\
ws-cleanup:latest\n\
ant:latest\n\
ace-editor:latest\n\
workflow-cps:latest\n\
workflow-job:latest\n\
workflow-basic-steps:latest\n\
gradle:latest\n\
pipeline-milestone-step:latest\n\
pipeline-input-step:latest\n\
pipeline-stage-step:latest\n\
pipeline-graph-analysis:latest\n\
pipeline-rest-api:latest\n\
pipeline-stage-view:latest\n\
pipeline-build-step:latest\n\
pipeline-model-api:latest\n\
pipeline-model-extensions:latest\n\
git-server:latest\n\
workflow-cps-global-lib:latest\n\
workflow-multibranch:latest\n\
docker-commons:latest\n\
docker-workflow:latest\n\
pipeline-stage-tags-metadata:latest\n\
pipeline-model-declarative-agent:latest\n\
pipeline-model-definition:latest\n\
lockable-resources:latest\n\
workflow-aggregator:latest\n\
github-api:latest\n\
github:latest\n\
github-branch-source:latest\n\
pipeline-github-lib:latest\n\
" >> $JENKINS_REF/plugins.txt
RUN /usr/local/bin/install-plugins.sh < $JENKINS_REF/plugins.txt

RUN apk add --no-cache --virtual make && \
    apk add --no-cache ca-certificates wget && \
    update-ca-certificates && \
    apk add --no-cache openssl

# install docker, docker-compose
ENV DOCKER_VERSION 17.10.0-ce-rc2
RUN curl -fL -o docker.tgz "https://download.docker.com/linux/static/test/x86_64/docker-$DOCKER_VERSION.tgz" && \
    tar --strip-components=1 -xvzf docker.tgz -C /usr/bin

RUN curl -o /usr/local/bin/docker-compose -L https://github.com/docker/compose/releases/download/1.19.1/docker-compose-`uname -s`-`uname -m` && chmod +x /usr/local/bin/docker-compose

# add docker group
RUN addgroup -S docker && adduser jenkins docker

VOLUME /var/jenkins

