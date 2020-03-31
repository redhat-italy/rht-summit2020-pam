FROM openjdk18-openshift

ENV AB_ENABLED off
ENV AB_JOLOKIA_AUTH_OPENSHIFT true

EXPOSE 8090

RUN mkdir -p /deployments/maven/repository/com/redhat/bank-loan/1.0.0

RUN curl http://${nexus-repo}/com/redhat/bank-loan/1.0.0/bank-loan-1.0.0.pom --output bank-loan-1.0.0.pom --silent
RUN curl http://${nexus-repo}/com/redhat/bank-loan/1.0.0/bank-loan-1.0.0.jar --output bank-loan-1.0.0.jar --silent

RUN mv bank-loan-1.0.0.pom /deployments/maven/repository/com/redhat/bank-loan/1.0.0
RUN mv bank-loan-1.0.0.jar /deployments/maven/repository/com/redhat/bank-loan/1.0.0

# Copy artifact
COPY target/bank-loan-service-1.0.0.jar /deployments/

USER root

RUN chmod -R 777 /deployments/maven/repository

USER jboss
