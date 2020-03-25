# dockerfile to build image for JBoss EAP 7

#start from eap72-openshift
FROM registry.redhat.io/jboss-eap-7/eap72-openshift

# Copy war to deployments folder
COPY jboss-test-webapp.war $JBOSS_HOME/standalone/deployments/

# User root to modify war owners
USER root

# Modify owners war
RUN chown jboss:jboss $JBOSS_HOME/standalone/deployments/jboss-test-webapp.war

# Important, use jboss user to run image
USER jboss
