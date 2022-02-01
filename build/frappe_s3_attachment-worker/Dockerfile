ARG IMAGE_TAG
ARG DOCKER_REGISTRY_PREFIX=frappe
FROM ${DOCKER_REGISTRY_PREFIX}/frappe-worker:${IMAGE_TAG}

ARG GIT_REPO=https://github.com/frappe/erpnext
ARG GIT_BRANCH

USER root
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    gcc \
    # For attachments-s3
    libmagic-dev \
    && rm -rf /var/lib/apt/lists/*

USER frappe
RUN install_app erpnext ${GIT_REPO} ${GIT_BRANCH}
RUN install_app frappe_s3_attachment https://github.com/Improwised/frappe_s3_attachment
# Only add the branch if you are using a specific tag or branch.
