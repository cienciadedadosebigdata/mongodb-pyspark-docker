FROM ubuntu:focal

#RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
#RUN apt-get update -y && apt-get install -y gnupg2 && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D68FA50FEA312927

RUN apt-get update -y && apt-get install -y gnupg2
RUN apt-key list | grep "expired: " | sed -ne 's|pub .*/\([^ ]*\) .*|\1|gp' | xargs -n1 apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B00A0BD1E2C63C11

RUN echo "deb https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-6.0.list
RUN apt-get install -y ca-certificates

RUN apt-get update -y && apt-get install -y mongodb-org && apt-get clean

RUN mkdir -p /data/db

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]
