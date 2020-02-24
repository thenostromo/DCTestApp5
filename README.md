A web-based "cats vs. dogs" voting app.
Here is a basic diagram of how the 5 services will work:

![diagram](./architecture.png)

Services:
- vote
    - bretfisher/examplevotingapp_vote
    - web front end for users to vote dog/cat

- redis
    - redis:3.2
    - key/value storage for incoming votes

- worker
    - bretfisher/examplevotingapp_worker:java
    - backend processor of redis and storing results in postgres

- db
    - postgres:9.4

- result
    - bretfisher/examplevotingapp_result
    - web app that shows results
 
 Deploy:
 1. Execute commands "docker-machine create node1 && docker-machine create node2 && docker-machine create node3";
 2. Connect to node1: docker-machine ssh node1
 3. Execute command on node1: "docker swarm init --advertise-addr [your-IP]"
 4. Execute command on node1 and past output to node2: "docker swarm join-token manager"
 5. Execute command on node1 and past output to node3: "docker swarm join-token manager"
 6. Execute command on node1: "docker stack deploy -c voting-app-stack.yml voteapp"
 
 Check here:
 `[your-IP]:5000` - vote app
 `[your-IP]:5001` - results of vote
 `[your-IP]:8080` - nodes visualization
