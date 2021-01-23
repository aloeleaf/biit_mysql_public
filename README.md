
This project for run very old mysql 4.0.27 docker image to save hardware resource and vmware resource.

1.) entrypoint.sh responsible to create mysql envirronment. 
Specify mysql root password: MYSQL_ROOT_PASSWORD=password

2.) build image
$ docker image build -t "name of image" .

3.) networking
To access directly from external vlan, create a new bridge
-- driver: ipvlan
-- subnet: set company vlan subnet
-- gateway: set company gateway
-- mode: layer 2 bridge
-- o: hosts network interface
$ docker network create -d ipvlan --subnet x.x.x.x/mask --gateway x.x.x.x  -o parent=ens192 -o mode=l2  net_ipvlan

4.) run
-- ip: ip address from company vlan
$ docker container run --network net_ipvlan -p 3306:3306 --ip x.x.x.x -v xxxx_biir_mysql:/usr/local/mysql/ --name xxxx_biir_mysql -e MYSQL_ROOT_PASSWORD=xxxxx biir_mysql
# biir_mysql
