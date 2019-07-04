# restart Docker
bash-3.2$
cd projects/dsp-deliver/
docker-compose down
docker-compose up -d
// docker-compose up -d --build
docker exec -u monitor -it dsp_monitor_1 run-monitor.sh

# remove

# another comands:
docker info
docker version
docker images
docker run hello-world
docker ps

# Switch to bash:
exec bash
# Switch to zsh:
exec zsh


curl -v localhost/dsp/health/v1
