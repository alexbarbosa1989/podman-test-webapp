# podman-test-webapp
wildfly/eap quickstart test on podman

1- Clone the project in your environment and perform mvn options to build the war:

$ git clone https://github.com/alexbarbosa1989/podman-test-webapp
$mvn clean install

2- Download the latest eap 7.2 image from Red Hat Registry https://access.redhat.com/containers/?tab=images#/registry.access.redhat.com/jboss-eap-7/eap72-openshift

3- Look if image is available aftet donwload to local registry:

~~~
$ podman images
REPOSITORY                                                 TAG      IMAGE ID       CREATED             SIZE
registry.redhat.io/jboss-eap-7/eap72-openshift             latest   435638adf5ff   About an hour ago        934 MB
~~~

3- 
