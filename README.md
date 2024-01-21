# Elastic_easy_install


Easy install and setup elasticsearch and kibana with its  Docker iamges 


1 - pull their images


```
docker pull elasticsearch && docker pull kibana

```


2 - run docker images 


```
docker run -d --name <elasticsearch> -p 9200:9200 -p 9300:9300 \
  -e "discovery.type=single-node" \
  -e "ELASTIC_USERNAME=<your_username>" \
  -e "ELASTIC_PASSWORD=<your_password>" \
  elasticsearch:<version>

```


```
docker run -d --name <kibana> -p 5601:5601 \
  -e "ELASTICSEARCH_HOSTS=http://localhost:9200" \
  docker.elastic.co/kibana/kibana:<version>

```


if both of them run successfully then open ``` http://localhost:5601``` and you will see this page 


![Screenshot from 2024-01-21 13-41-42](https://github.com/hosseinhj1380/Elastic_easy_install/assets/113828873/20218d0a-79c3-41b7-a458-cde48e1c321e)


now with ``` docker ps ```  command you can see your containers and its ID 


copy elasticsearch containerID and then ``` docker exec -it <containerID> bash ``` and you can now see your inside container 

and then run this command  ``` bin/elasticsearch-create-enrollment-token --scope kibana ``` 

this command will generate a key that kibana will match with that to the elasticsearch 

copy the key and paste it on kibana on ``` http://localhost:5601``` 

if its gonna be ok kibana will want a verification code from you and you can acces that code with these way 

copy containerID of kibana as told before and then 

``` docker exec -it <container ID> bash ``` 

and then run this command in container bash mode ``` bin/kibana-verification-code  ``` 


and copy the code and paste it on browser page 

WAIT until connecion completed and then you see login page and you can login with your ```<username >``` and ```<password>```
