ARG ERPIMAGE
FROM frappe/erpnext-worker:$ERPIMAGE
USER root
RUN sed -i 's/^PASS_MAX_DAYS.*/PASS_MAX_DAYS    -1/' /etc/login.defs && \
    sed -i 's/^PASS_MIN_DAYS.*/PASS_MIN_DAYS    -1/' /etc/login.defs
USER frappe
RUN install_app frappe_s3_attachment https://github.com/Improwised/frappe_s3_attachment
# Only add the branch if you are using a specific tag or branch.
