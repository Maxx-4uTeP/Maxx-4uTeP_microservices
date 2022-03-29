## GITLAB CI

# new vm
yc compute instance create \
  --name gitlab-ci-vm \
  --platform standard-v2 \
  --memory 8GB \
  --cores 2 \
  --core-fraction 100 \
  --preemptible \
  --zone ru-central1-a \
  --network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \
  --create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1804-lts,size=30 \
  --ssh-key ~/.ssh/id_rsa.pub
# 11
docker-machine create \
  --driver generic \
  --generic-ip-address=62.84.124.102 \
  --generic-ssh-user yc-user \
  --generic-ssh-key ~/.ssh/id_rsa \
  docker-gitlab 

# 12
ssh yc-user@62.84.124.102

sudo -i
mkdir -p /srv/gitlab/config /srv/gitlab/data /srv/gitlab/logs
cd /srv/gitlab
touch docker-compose.yml
nano docker-compose.yml
# 13
web:
  image: 'gitlab/gitlab-ce:latest'
  restart: always
  hostname: 'gitlab.example.com'
  environment:
    GITLAB_OMNIBUS_CONFIG: |
      external_url 'http://62.84.124.102'
  ports:
    - '80:80'
    - '443:443'
    - '2222:22'
  volumes:
    - '/srv/gitlab/config:/etc/gitlab'
    - '/srv/gitlab/logs:/var/log/gitlab'
    - '/srv/gitlab/data:/var/opt/gitlab'


# 14

apt install docker-compose
docker-compose up -d

# 17
http://62.84.124.102
login: root
Password:
sudo docker exec -it 4c385a834f51 grep 'Password:' /etc/gitlab/initial_root_password


# 25
exit
exit

git checkout -b gitlab-ci-1
git remote add gitlab http://62.84.124.102/homework/example.git
git push gitlab gitlab-ci-1

git add .gitlab-ci.yml
git commit -m 'add pipeline definition'
git push gitlab gitlab-ci-1

# 28
ssh yc-user@62.84.124.102
sudo -i
cd /srv/gitlab
docker run -d \
  --name gitlab-runner \
  --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest

# 29
docker exec -it gitlab-runner gitlab-runner register \
    --url http://62.84.124.102/ \
    --non-interactive \
    --locked=false \
    --name DockerRunner \
    --executor docker \
    --docker-image alpine:latest \
    --registration-token sG19yeJsdgzYsGxxjQA3 \
    --tag-list "linux,xenial,ubuntu,docker" \
    --run-untagged

# 32
git clone https://github.com/express42/reddit.git && rm -rf ./reddit/.git
git add reddit/
git commit -m "Add reddit app"
git push gitlab gitlab-ci-1

# 36
git commit -am "page 36"
git push gitlab gitlab-ci-1


