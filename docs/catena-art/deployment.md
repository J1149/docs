# PAI Pass Production Process

So the simplified version is,

- I develop code
- I test it locally
- I commit the changes then push them to github
- I build an image, tag it and push it to ecr
- I make a new revision of the task definition
- I update the service to point to the new task definition 

### Tag and Push

You can change the tag by modifying

```_docker_tag_name```

in

```/catena/ops/to_aws/from_docker/push.py```

and then running that file.

Note, you need the following env variables set for that script to run properly:

- AWS_ACCESS_KEY=
- AWS_SECRET_ACCESS_KEY=
- AWS_ACCOUNT_ID=
- AWS_REGION=us-east-2
- AWS_PROJECT=catena
- DOCKER_COMPOSE_YML_INPUT=/DIRECTORY_WHERE_CATENA_IS_STORED/catena/docker-compose.staging.yml

### Edit Task Definition

You can then create a new task revision to point to the image you tagged here

[https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/taskDefinitions/catena-backend](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/taskDefinitions/catena-backend)

### Update Service

Then you can update the service to point at the new task definition by going here

[https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/clusters/catena/services/catena-backend/update](https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/clusters/catena/services/catena-backend/update)

