# dockerfile to build image for JBoss EAP 7

#start from eap72-openshift
#registry.redhat.io/jboss-eap-7/eap72-openshift
FROM registry.redhat.io/jboss-eap-7/eap74-openjdk11-openshift-rhel8

# Copy war to deployments folder
COPY jboss-test-webapp.war $JBOSS_HOME/standalone/deployments/

# User root to modify war owners
USER root

# Modify owners war
RUN chown jboss:jboss $JBOSS_HOME/standalone/deployments/jboss-test-webapp.war

# Important, use numeric user user to run image in Kubernetes/Openshift. Other containerized env can run with another user i. e., jboss
USER 1001
