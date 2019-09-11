FROM alpine:latest

# L'adresse e-amil existe, même mot de passe que mon debian alienware, en remplaçant arobase par [at], en minuscules.
LABEL maintainer="Jean-Baptiste Lasselle <jean.baptiste.lasselle.omega.io@gmail.com>"
LABEL vendor="omega.io"

LABEL project="https://github.com/Jean-Baptiste-Lasselle/omega"
LABEL product="Static Site generator for the offical website of the https://github.com/Jean-Baptiste-Lasselle/omega project"
LABEL product-type="Static Site generator for an offical Open Source project Website"
LABEL gone-hugo="https://jean-baptiste-lasselle.github.io/omega/"

ARG HUGO_DESIRED_VERSION=0.40
ENV HUGO_DESIRED_VERSION=$HUGO_DESIRED_VERSION


# That's where the HUGO EXECTUABLE SHOULD BE FOUND
ARG HUGO_INSTALLATION_PATH=/usr/bin/hugo

# Well the original seemed to have 
# ENV HUGO_VERSION=0.40

RUN apk update && apk add --no-cache git openssl py-pygments curl \
    && curl -L https://github.com/gohugoio/hugo/releases/download/v${HUGO_DESIRED_VERSION}/hugo_${HUGO_DESIRED_VERSION}_Linux-64bit.tar.gz | tar -xz \
    && mv hugo ${HUGO_INSTALLATION_PATH} \
    && apk del curl

# 
# Well this user will run the Hugo commands inside the container
# https://github.com/gliderlabs/docker-alpine/issues/38#issuecomment-339400260
# 

ARG PEGASUS_OPERATOR_USER_ID=1003
ARG PEGASUS_OPERATOR_USER_NAME=pegasus
ENV PEGASUS_OPERATOR_USER_NAME=$PEGASUS_OPERATOR_USER_NAME

ARG PEGASUS_OPERATOR_GROUP_ID=1022
ARG PEGASUS_OPERATOR_GROUP_NAME=zodiac
ENV PEGASUS_OPERATOR_GROUP_NAME=$PEGASUS_OPERATOR_GROUP_NAME

RUN addgroup -g ${PEGASUS_OPERATOR_GROUP_ID} ${PEGASUS_OPERATOR_GROUP_NAME} && \
    adduser -D -u ${PEGASUS_OPERATOR_USER_ID} -G ${PEGASUS_OPERATOR_GROUP_NAME} ${PEGASUS_OPERATOR_USER_NAME} -h /home/${PEGASUS_OPERATOR_USER_NAME}


RUN echo "export PATH=\$PATH:/usr/bin/hugo" >> /home/${PEGASUS_OPERATOR_USER_NAME}/.shrc



ARG HUGO_WORKSPACE_INSIDE_CONTAINER=/usr/share/hugo/workspace
ENV HUGO_WORKSPACE_INSIDE_CONTAINER=$HUGO_WORKSPACE_INSIDE_CONTAINER


# export HUGO_WORKSPACE_INSIDE_CONTAINER=/usr/share/hugo/workspace
RUN mkdir -p $HUGO_WORKSPACE_INSIDE_CONTAINER
# RUN chown -R $PEGASUS_OPERATOR_USER_NAME:$PEGASUS_OPERATOR_GROUP_NAME $HUGO_WORKSPACE_INSIDE_CONTAINER




USER $PEGASUS_OPERATOR_USER_NAME

WORKDIR $HUGO_WORKSPACE_INSIDE_CONTAINER

# RUN echo "Cette phrase a été ajoutée au cours du processus de build de l'image Docker, par le user [$(whoami)], dans le fichier [./.pegasus.logs], dans le répertoire [$(pwd)] " >> ./.pegasus.logs

RUN whoami
RUN cat ~/.shrc
RUN source ~/.shrc &&  hugo version && hugo help

# 1313 is Hugo server's default port number
EXPOSE 1313

CMD ["/bin/sh"]
