# Azure DevOps self hosted base image

- https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops

# Set variables

```bash
IMAGE_NAME="azdevops-base-image"
IMAGE_TAG="1.0.0"
AZP_URL=$AZP_URL                  # <Azure DevOps instance>
AZP_TOKEN=$AZP_TOKEN              # <PAT token>
AZP_AGENT_NAME="docker-agent"     # <agent name>
```

## Environment variables

| Environment variable | Description                                                                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| AZP_URL              | The URL of the Azure DevOps or Azure DevOps Server instance.                                                                             |
| AZP_TOKEN            | Personal Access Token (PAT) with Agent Pools (read, manage) scope, created by a user who has permission to configure agents, at AZP_URL. |
| AZP_AGENT_NAME       | Agent name (default value: the container hostname).                                                                                      |
| AZP_POOL             | Agent pool name (default value: Default).                                                                                                |
| AZP_WORK             | Work directory (default value: \_work).                                                                                                  |

# Build image

### Base image Ubuntu 20.04

```
docker build -t $IMAGE_NAME:$IMAGE_TAG -f Dockerfile-ubuntu2004 .
docker build -t $IMAGE_NAME:$IMAGE_TAG-slim -f Dockerfile-ubuntu2004-slim .
```

### Base image Ubuntu 22.04

```
docker build -t $IMAGE_NAME:$IMAGE_TAG -f Dockerfile-ubuntu2204 .
docker build -t $IMAGE_NAME:$IMAGE_TAG-slim -f Dockerfile-ubuntu2204-slim .
```

# Start image

```
docker run --name agent1 --rm -e AZP_URL=$AZP_URL -e AZP_TOKEN=$AZP_TOKEN -e AZP_AGENT_NAME=$AZP_AGENT_NAME $IMAGE_NAME:$IMAGE_TAG
```

# Exec image

```
docker exec -it agent1 /bin/bash
```
