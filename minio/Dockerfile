################################################################################
#                                 Minio Container                              #
################################################################################

FROM centos:centos7
MAINTAINER The METIS Project <noreply@nowhere.com>
LABEL version="release-0.1.0" description="METIS Minio Pod"

# Declare Build Args
ARG MINIO_ACCESS_KEY
ARG MINIO_SECRET_KEY
ENV MINIO_ACCESS_KEY ${MINIO_ACCESS_KEY}
ENV MINIO_SECRET_KEY ${MINIO_SECRET_KEY}
ENV MINIO_DOWNLOAD_URL="https://dl.minio.io/server/minio/release/linux-amd64/minio"

# Install Software
RUN mkdir -p /minio/bin \
 && yum update -y \
 && yum install -y curl \
 && yum clean all \
 && curl -o /minio/bin/minio $MINIO_DOWNLOAD_URL \
 && chmod +x /minio/bin/minio

# Create Volumes
VOLUME ["/minio/data", "/minio/config"]

# Use following when OpenShift anyuid is allowed
# Set Permissions
# RUN chown 1001:0 -R /minio \
#  && chmod -R g+rwX  /minio
# Run as user
# USER 1001

# Document Exposed Ports
EXPOSE 9000

CMD ["/minio/bin/minio", "server", "--config-dir=/minio/config", "/minio/data"]