docker service create --name redis redis:7.4.1

<b><mark>docker service create --mode global --name redis2 redis:7.4.1</mark></b><br>

docker service ls

docker service create --name redis --replicas=5 redis:7.4.1

docker service create --name redis --secret secret.json redis:7.4.1

docker service create --name redis \
    --secret source=ssh-key,target=ssh \
    --secret source=app-key,target=app,uid=1000,gid=1001,mode=0400 \
    redis:7.4.1

docker service create --name=redis --config redis-conf redis:7.4.1

<b><mark>docker service create --name my_service --constraint 'node.labels.role==frontend' nginx:latest</mark></b><br>


docker service create --replicas 10 --name redis --update-delay 10s --update-parallelism 2 redis:7.4.1

docker service create --name redis_2 --replicas 5 --env MYVAR=foo --env MYVAR2=bar redis:7.4.1

<b><mark>docker service create --name redis --hostname myredis redis:7.4.1</mark></b><br>

docker service create --name redis_2 --label com.example.foo="bar" --label bar=baz redis:7.4.1

docker service create --name my-service --replicas 3 
--mount type=volume,source=my-volume,destination=/path/in/container,volume-label="color=red",volume-label="shape=round" nginx:alpine

docker service create --name my-service --replicas 3 --mount type=volume,destination=/path/in/container nginx:alpine

docker service create --name my-service --mount type=bind,source=/path/on/host,destination=/path/in/container nginx:alpine

<b><mark>docker service create --name redis_2 --mode global redis:7.4.1</mark></b><br>
//replicated service belirtilen sayıda görev çalıştırır.<br>
//global service ise swarm üzerinde her node üstünde çalışır.<br>

docker service create --name redis_2 --constraint node.platform.os==linux --constraint node.labels.type==queue redis:7.4.1

<b><mark>docker service create --reserve-memory=4GB --name=too-big nginx:alpine</mark></b><br>

<b><mark>docker service create --limit-memory=4GB --name=too-big nginx:alpine</mark></b><br>

docker service create --name nginx --replicas 2 --replicas-max-per-node 1 --placement-pref 'spread=node.labels.datacenter' nginx



docker network create --driver overlay my-network
docker service create --replicas 3 --network my-network --name my-web nginx

docker service create --name my_web --replicas 3 --publish 8080:80 nginx

docker service create --name my_web --replicas 3 --publish published=8080,target=80 nginx

docker service create --name myjob --mode replicated-job bash "true"

A replicated job is like a replicated service. 
Setting the --replicas flag will specify total number of iterations of a job to execute.

docker service create --name mythrottledjob --mode replicated-job --replicas 10 --max-concurrent 2 bash "true"

By default, all replicas of a replicated job will launch at once. 
To control the total number of replicas that are executing simultaneously at any one time, the --max-concurrent flag can be used:

docker service inspect --pretty

docker service logs --details myFirstService

docker service logs --since timestampDegeri --tail 5 --timestamps --follow myFirstService

docker service ls --format table

docker service ls --filter name=frontend

docker service ls --quiet 
//sadece idleri görüntüler.

docker service ps

docker service rm reedis

docker service rollback

docker service scale 

docker service scale backend=20

docker service update --replicas=50 frontend

-args		Service command args
--cap-add		API 1.41+ Add Linux capabilities
--cap-drop		API 1.41+ Drop Linux capabilities
--config-add		API 1.30+ Add or update a config file on a service
--config-rm		API 1.30+ Remove a configuration file
--constraint-add		Add or update a placement constraint
--constraint-rm		Remove a constraint
--container-label-add		Add or update a container label
--container-label-rm		Remove a container label by its key

--health-cmd		API 1.25+ Command to run to check health
--health-interval		API 1.25+ Time between running the check (ms|s|m|h)
--health-retries		API 1.25+ Consecutive failures needed to report unhealthy
--health-start-interval		API 1.44+ Time between running the check during the start period (ms|s|m|h)
--health-start-period		API 1.29+ Start period for the container to initialize before counting retries towards unstable (ms|s|m|h)
--health-timeout		API 1.25+ Maximum time to allow one check to run

--restart-condition		Restart when condition is met (none, on-failure, any)
--restart-delay		Delay between restart attempts (ns|us|ms|s|m|h)
--restart-max-attempts		Maximum number of restarts before giving up
--restart-window		Window used to evaluate the restart policy

--update-failure-action		Action on update failure (pause, continue, rollback)
--update-max-failure-ratio		API 1.25+ Failure rate to tolerate during an update

--rollback-delay		API 1.28+ Delay between task rollbacks (ns|us|ms|s|m|h)
--rollback-failure-action		API 1.28+ Action on rollback failure (pause, continue)
--rollback-max-failure-ratio		API 1.28+ Failure rate to tolerate during a rollback
--rollback-monitor		API 1.28+ Duration after each task rollback to monitor for failure 

