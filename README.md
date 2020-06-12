# podman-test-webapp
wildfly/eap quickstart test on podman.

1- Clone the project in your environment and perform mvn options to build the war:

~~~
$ git clone https://github.com/alexbarbosa1989/podman-test-webapp

$mvn clean install
~~~

2- Move generated war to /docker dir or edit Dockerfile pointing to war path:
~~~
mv ${PROJECT_HOME}/target/jboss-test-webapp.war ${PROJECT_HOME}/docker/
~~~

3- Download the latest eap 7.2 image from Red Hat Registry https://access.redhat.com/containers/?tab=images#/registry.access.redhat.com/jboss-eap-7/eap72-openshift

4- Look if image is available aftet donwload to local registry:

~~~
$ podman images
REPOSITORY                                                 TAG      IMAGE ID       CREATED                  SIZE
registry.redhat.io/jboss-eap-7/eap72-openshift             latest   435638adf5ff   About an hour ago        934 MB
~~~

5- Build the image with the Dockerfile:

~~~
$ podman build -t abarbosa/eaptest:1.0 ${PROJECT_HOME}/docker
~~~

6- Review if image abarbosa/eaptest:1.0 was created (make sure to write the tag in lowercase):

~~~
[abarbosa@localhost ~]$ podman images
REPOSITORY                                                 TAG      IMAGE ID       CREATED              SIZE
localhost/abarbosa/eaptest                                 1.0      dace9d7ed592   About an hour ago    934 MB
registry.redhat.io/jboss-eap-7/eap72-openshift             latest   435638adf5ff   About an hour ago    934 MB
~~~

7- Create the podman image with the recent created image making available bind to 8080 port:

~~~
 podman run -it -p 8080:8080 localhost/abarbosa/eaptest:1.0
~~~

8- Validate the podman container process is now available using **podman ps**:

~~~
CONTAINER ID  IMAGE                           COMMAND               CREATED        STATUS            PORTS                   NAMES
eaf051a0b0db  localhost/abarbosa/eaptest:1.0  /opt/eap/bin/open...  7 seconds ago  Up 7 seconds ago  0.0.0.0:8080->8080/tcp  youthful_banzai
~~~

9- Restart local machine firewall to allow communication between localhost and the new container:

~~~
$ sudo systemctl restart firewalld
~~~

10- Test the deployed war service:

~~~
$curl localhost:8080/jboss-test-webapp
~~~
