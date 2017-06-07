FROM oraclelinux:7-slim

LABEL maintainer "Haiwei Liu <carllhw@gmail.com>"

# Common environment variables required for this build (do NOT change)
# --------------------------------------------------------------------
ENV ORACLT_PKG1=oracle-instantclient11.2-basic-11.2.0.2.0.x86_64.rpm \
    ORACLT_PKG2=oracle-instantclient11.2-sqlplus-11.2.0.2.0.x86_64.rpm

# Copy packages
# -------------
COPY $ORACLT_PKG1 \
      $ORACLT_PKG2 \
      /u01/

# Setup filesystem and oracle user, install
# ------------------------------------------------------------
RUN mkdir -p /u01/oracle && \
    useradd -u 1000 -b /u01 -M -s /bin/bash oracle && \
    chown oracle:oracle /u01 /u01/oracle && \
    yum localinstall -y /u01/$ORACLT_PKG1 /u01/$ORACLT_PKG2 && \
    rm -f /u01/$ORACLT_PKG1 /u01/$ORACLT_PKG2 && \
    yum clean all

USER oracle
ENV PATH=/usr/lib/oracle/11.2/client64/bin:$PATH \
    LD_LIBRARY_PATH=/usr/lib/oracle/11.2/client64/lib:$LD_LIBRARY_PATH
WORKDIR /u01/oracle

ENTRYPOINT /bin/bash
