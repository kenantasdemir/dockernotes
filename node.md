docker swarm init

docker swarm join-token worker

docker swarm leave

docker node ls --filter "label=foo"
docker node ls --format table

docker node rm swarmNode

<b><mark>docker node promote nodeName</mark></b><br>
//node'u manager olarak yükseltir.

<b><mark>docker node demote nodeName</mark></b><br>
//manager node'u normal node'a çevirir.

docker node inspect nodeName

docker node update --label-add foo worker1

docker node update --label-add foo --label-add bar worker

docker node update --label-rm foo worker

docker node update nodeName --role manager

docker node update --label-add type=queue worker1
