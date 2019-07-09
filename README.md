# create a docker swarm:

1. flash raspbian images and turn on pis

2. find ip / mac addresses

2. update inventory and vars.yml

3. check connection with: 

    $ ansible pis -k -i inventory -m ping

4. provision pis: 

    $ ansible-playbook -k -i inventory provision.yml

5. init the swarm cluster: 
    
    $ sudo docker swarm init --advertise-addr [ 1ST NODE IP ADDRESS ]

6. run the join command on the other nodes

7. start visualizer on the manager node:

    $ docker service create \
    --name=viz \
    --publish=8080:8080/tcp \
    --constraint=node.role==manager \
    --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
    alexellis2/visualizer-arm:latest