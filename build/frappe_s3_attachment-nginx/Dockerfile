ARG NODE_IMAGE_TAG=14-buster-slim
ARG DOCKER_REGISTRY_PREFIX=frappe
ARG IMAGE_TAG

FROM node:${NODE_IMAGE_TAG}

ARG GIT_REPO=https://github.com/frappe/erpnext
ARG GIT_BRANCH
ARG FRAPPE_BRANCH

COPY install_app.sh /install_app
RUN chmod +x /install_app && \
  apt-get update -y && \
  apt-get install build-essential git python2 -y && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

RUN /install_app erpnext ${GIT_REPO} ${GIT_BRANCH} ${FRAPPE_BRANCH}
RUN /install_app frappe_s3_attachment https://github.com/Improwised/frappe_s3_attachment "" ${FRAPPE_BRANCH}

FROM ${DOCKER_REGISTRY_PREFIX}/frappe-nginx:${IMAGE_TAG}

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync
RUN echo "erpnext\nfrappe_s3_attachment" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
