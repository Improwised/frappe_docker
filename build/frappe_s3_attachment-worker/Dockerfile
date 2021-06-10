ARG IMAGE_TAG=v13.4.1
ARG DOCKER_REGISTRY_PREFIX=frappe
FROM ${DOCKER_REGISTRY_PREFIX}/frappe-worker:${IMAGE_TAG}

ARG GIT_REPO=https://github.com/frappe/erpnext
ARG GIT_BRANCH=v13.4.1

RUN install_app erpnext ${GIT_REPO} ${GIT_BRANCH}
RUN install_app frappe_s3_attachment https://github.com/Improwised/frappe_s3_attachment
# Only add the branch if you are using a specific tag or branch.
