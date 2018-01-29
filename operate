clear_images
#!/usr/bin/env bash
docker ps -a | awk  '{print $1}' |xargs docker rm -f
docker images |grep -v swarm |awk '{print $3}' |xargs docker rmi -f

---docker  images 需要账号密码部署----------
docker stack deploy -c 11.yaml 11 --with-registry-auth
