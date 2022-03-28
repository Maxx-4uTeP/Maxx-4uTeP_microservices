# MONITORING

# 4
yc compute instance create \
  --name docker-host \
  --platform standard-v2 \
  --memory 8GB \
  --cores 2 \
  --core-fraction 100 \
  --preemptible \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --ssh-key ~/.ssh/id_rsa.pub

# 5
docker-machine ls
docker-machine rm MACHINE_NAME


docker-machine create \
  --driver generic \
  --generic-ip-address=178.154.204.34 \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/id_rsa \
  docker-host

eval $(docker-machine env docker-host)

# 6
docker run --rm -p 9090:9090 -d --name prometheus  prom/prometheus

docker ps
docker-machine ip docker-host

# 14
docker stop prometheus

# 19
cd monitoring/prometheus
export USER_NAME=4utep
docker build -t $USER_NAME/prometheus .

# 21
cd ../..
for i in ui post-py comment; do cd src/$i; bash docker_build.sh; cd -; done

# 24

docker-compose up -d

# 31
docker-compose stop post

# 45
cd ~/devops/Maxx-4uTeP_microservices/monitoring/prometheus
docker build -t $USER_NAME/prometheus .

# 46
cd ~/devops/Maxx-4uTeP_microservices/docker
docker-compose down
docker-compose up -d

# 48
docker-machine ssh docker-host
yes > /dev/null

# 49
docker login

docker push 4utep/ui
docker push 4utep/comment
docker push 4utep/post
docker push 4utep/prometheus

docker-machine rm docker-host
yc compute instance delete docker-host

