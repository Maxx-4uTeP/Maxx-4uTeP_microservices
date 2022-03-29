## LOGGING

# 5

docker login
export USER_NAME='4utep'
cd ./src/ui && bash docker_build.sh && docker push $USER_NAME/ui
cd ../post-py && bash docker_build.sh && docker push $USER_NAME/post
cd ../comment && bash docker_build.sh && docker push $USER_NAME/comment
cd ../..

# 6 - 8
docker-machine ls
docker-machine rm MACHINE_NAME -f

docker-machine create \
    --driver yandex \
    --yandex-image-family "ubuntu-1804-lts" \
    --yandex-platform-id "standard-v1" \
    --yandex-folder-id $FOLDER_ID \
    --yandex-sa-key-file $SA_KEY_PATH \
    --yandex-preemptible=true \
    --yandex-nat=true \
    --yandex-memory "8" \
    logging

eval $(docker-machine env logging)
docker-machine ip logging

51.250.65.122

# 14
cd logging/fluentd && docker build -t $USER_NAME/fluentd . && docker push $USER_NAME/fluent

# 17
cd ../../docker && docker-compose up -d
docker-compose logs -f post

# 20
docker-compose -f docker-compose-logging.yml up -d
docker-compose down
docker-compose up -d

http://51.250.65.122
http://51.250.65.122:5601

# 25
fluentd-*

# 34
cd ../logging/fluentd && docker build -t $USER_NAME/fluentd . && docker push $USER_NAME/fluentd
cd ../../docker && docker-compose -f docker-compose-logging.yml up -d fluentd

# 41 
docker-compose stop ui
docker-compose rm ui
docker-compose up -d

# 44
cd ../logging/fluentd && docker build -t $USER_NAME/fluentd .
cd ../../docker && docker-compose -f docker-compose-logging.yml up -d fluentd





# ENDGAME
docker-machine rm logging -f



cd ../logging/fluentd         
docker build -t $USER_NAME/fluentd .
cd ../../docker 
docker-compose up -d fluentd
docker-compose logs -f fluentd


2022-03-24 10:06:46 +0000 fluent.warn: {"next_retry":"2022-03-24 10:15:49 +0000","error_class":"NameError","error":"uninitialized constant Elasticsearch::Transport","plugin_id":"object:2afbd4146c5c","message":"temporarily failed to flush the buffer. next_retry=2022-03-24 10:15:49 +0000 error_class=\"NameError\" error=\"uninitialized constant Elasticsearch::Transport\" plugin_id=\"object:2afbd4146c5c\""}







