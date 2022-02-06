# Maxx-4uTeP_microservices
Maxx-4uTeP microservices repository

yc compute instance create \
  --name docker-host \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=15 \
  --ssh-key ~/.ssh/id_rsa.pub
	
docker-machine create \
  --driver generic \
  --generic-ip-address=62.84.126.0 \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/id_rsa \
  docker-host
  
eval $(docker-machine env docker-host)


docker build -t reddit:latest .

docker run --name reddit -d --network=host reddit:latest

docker-machine ls

docker login

docker tag reddit:latest 4utep/otus-reddit:1.0

docker push 4utep/otus-reddit:1.0

docker run --name reddit -d -p 9292:9292 4utep/otus-reddit:1.0


