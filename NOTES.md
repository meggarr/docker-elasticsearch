# Build Docker image
docker build -t docker.calix.local:18080/docker-elasticsearch:6.5.4-calix .

# Change vm max count
sysctl -w vm.max_map_count=262144

# Run Docker
docker run --detach --name elasticsearch \
    --privileged --network host \
	-e CLUSTER_NAME=es-cluster-1 \
	-e NODE_NAME=rmeng-1 \
	-e NETWORK_HOST=0.0.0.0 \
	-e DISCOVERY_HOSTS=192.168.38.202,192.168.38.228 \
	docker.calix.local:18080/docker-elasticsearch:6.2.2-calix

