WebLogic 10.3.6. on Docker
==========================

* Create the image.

	cd OracleWebLogic/dockerfiles
	./buildDockerImage.sh -v 10.3.6 -d

* Verify the docker image

	docker images

you should see something like this:

	REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
	oracle/weblogic     10.3.6-dev          81f58771358b        2 minutes ago       2.01 GB

* Installing weblogic 10.3.6 and create another custom image

	cd OracleWeblogic/samples/11g-domain
	docker build -t oracle/weblogic:10.3.6-dev-custom .

* Verify the docker image

	docker images

you should see something like this:

	REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
	oracle/weblogic     10.3.6-dev-custom   9ffffd180f6c        3 seconds ago       2.011 GB
	oracle/weblogic     10.3.6-dev          81f58771358b        2 minutes ago       2.01 GB


* Create the container

	docker run --name wlsadmin -d -i oracle/weblogic:10.3.6-dev-custom 

* Verify that the container is running

	docker ps

you should see something like this:

	CONTAINER ID        IMAGE                               COMMAND              CREATED             STATUS              PORTS                          NAMES
	73a1298ac30c        oracle/weblogic:10.3.6-dev-custom   "startWebLogic.sh"   3 seconds ago       Up 2 seconds        5556/tcp, 7001/tcp, 7002/tcp   wlsadmin 

* Connect to the container

	docker exec -i -t wlsadmin /bin/bash

* Connect to the weblogic console

	http://<ip-docker>:7001/console
	username: weblogic
	password: welcome1
