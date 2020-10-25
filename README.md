# Using docker compose and ECS
This is just a repo to document my study of Amazon ECS and docker compose.

I'm following this [AWS tutorial](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-cli-tutorial-ec2.html).

## Useful links:
Here is how to define [install ecs-cli](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html).

The ecs-cli command line [reference](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_reference.html).

The possible [parameters](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cmd-ecs-cli-compose-ecsparams.html) for the `ecs-params.yml` file.

## Personal conclusions
The ecs-cli allows to define **ECS Task Definitions** from a `docker-compose.yml` file which specifies the containers orchestration; And `ecs-params.yml` which augmentates the compose file to add AWS ECS specific configurations for task definitions and some run parameters for tasks and services.

However the `ecs-params.yml` doesn't hold information to run the service behind a load balancer. For that you need to use this command.

```bash
ecs-cli compose service up \
--target-group-arn "arn:aws:elasticloadbalancing:us-east-1:xxxxxxxx:targetgroup/awsvpc-nginx/2bf8921935c827bd" \
--container-name nginx --container-port 80
```

See this, StackOverflow [thread](https://stackoverflow.com/questions/53898568/ecs-cli-compose-service-up-with-a-load-balancer) for more details.

To extract the full power of this cli tool it is recommended to have first an understanding of the AWS ECS service.
