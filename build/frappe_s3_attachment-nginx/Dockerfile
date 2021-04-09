FROM bitnami/node:12-prod
RUN sed -i 's/^PASS_MAX_DAYS.*/PASS_MAX_DAYS    -1/' /etc/login.defs && \
    sed -i 's/^PASS_MIN_DAYS.*/PASS_MIN_DAYS    -1/' /etc/login.defs
COPY ./install_app.sh /install_app
RUN install_packages git phantomjs
RUN /install_app frappe_s3_attachment https://github.com/Improwised/frappe_s3_attachment

FROM frappe/erpnext-nginx:v13.0.1
RUN sed -i 's/^PASS_MAX_DAYS.*/PASS_MAX_DAYS    -1/' /etc/login.defs && \
    sed -i 's/^PASS_MIN_DAYS.*/PASS_MIN_DAYS    -1/' /etc/login.defs
COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync
RUN echo -n "\nfrappe_s3_attachment" >> /var/www/html/apps.txt
VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
