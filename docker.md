- In the same spirit as `gst` for `git status` I prefer having a `dps` for `docker ps`

```bash
alias dps="docker ps"
```

- Many a times my environment is full of unwanted containers, and I can't remember how to delete all of them. So here we go

```bash
function removeAllDockerContainers {
  docker rm -f $(docker ps -aq)
}
```

- In similar spirit as above

```bash
killAllDockerContainers() {
	docker kill $(docker ps -q)
}
```

- If I only want to delete the stopped containers

```bash
deleteAllStoppedDockerContainers() {
	docker rm $(docker ps -a -q)
}
```

- Many a times I want to `bash` or if there is no `bash` then `sh` into one of the many running containers. And writing the whole command `docker exec -it <container id> bash` is a bit of pain for my fingers. So, I have a nice little menu printed where I can simply select the container I want to `sh` or `bash` into. I have the same thing configured for killing a container too. 

```bash
execBashInDocker() {
	docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl
	echo "Which docker container to bash into?"
	read sequenceNumber
	dockerContainerId=`docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl | awk -v sequenceNumber="$sequenceNumber" "NR == sequenceNumber" | awk '{print $2}'`
	docker exec -it $dockerContainerId /bin/bash
}

execShInDocker() {
	docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl
        echo "Which docker container to sh into?"
        read sequenceNumber
        dockerContainerId=`docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl | awk -v sequenceNumber="$sequenceNumber" "NR == sequenceNumber" | awk '{print $2}'`
        docker exec -it $dockerContainerId sh
}

killADockerContainer() {
        docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl
        echo "Which docker container you want to kill?"
        read sequenceNumber
        dockerContainerId=`docker ps --format "{{ .ID }} ,  {{ .Image }}" | sort -nr| nl | awk -v sequenceNumber="$sequenceNumber" "NR == sequenceNumber" | awk '{print $2}'`
        docker container kill $dockerContainerId
}
```