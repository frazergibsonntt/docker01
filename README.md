# docker01
web and db containers on a local VM

Quickstart:
1. mkdir a keys folder
2. key-gen a key pair
3. vagrant up the docker machine
4. ssh -i keys/id_rsa vagrant@10.0.0.10 into the machine
5. Check port forwarding works
6. docker image build -t tomcatimage:1.0 /vagrant/tomcat
7. docker image build -t dbimage:1.0 /vagrant/db --build-arg db_root_pass=admin123 --build-arg db_pass=todo123
8. docker network create webstack
9. docker run --net=webstack --name=tomcatcont -d -p 8080:8080 <tomcat image id>
10. docker run --net=webstack --name=dbcont -d <db image id>
11. docker exec -it tomcatcont /bin/bash
12. ping dbcont
13. telnet dbcont 3306

All working.

