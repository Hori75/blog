---
layout: post
title:  "Simple Development and Deployment Using Docker"
author: hori75
date:   2022-05-07 12:00:00 +0700
background: '/images/docker-compose.png'
excerpt_separator: <!--more-->
---

As more and more services created, we need to manage the development and deployment in scalable way.
<!--more-->
But, we also need to make it portable. 
This becomes a challenge that needs to be solve in a simple way (at least in current project)
Docker is an easy way to store builds and deploy.

### Docker Usage

Docker automates application build and setup and stores the result in form of **image**. 
Docker will run commands based on the project `Dockerfile`.
This **image** later could be run as container or store it in image registry to be pulled and run.

**Container** is a standard, lightweight, and secure software that contains anything it needs to operate.
Due to that characteristic, we could use Docker to run our server basically anywhere as long docker could be used and the image is obtained.
**Container** is isolated from the main system so we could have many of them running on an instance without interfering each other.

#### Example: build image and deploy to a server

In this example, we use java springboot so we could use grade to build image for us.
So we build the image via `./gradlew bootBuildImage`, tag the image and push it into an image registry as latest.
For example check this snippet about the job below (from `.gitlab-ci.yml`), you could run it manually to try
(after filling the env variables of course).

```
PublishStaging:
    stage: Publish
    image: docker:latest
    before_script:
        - docker login -u _json_key --password-stdin https://$IMAGE_REGISTRY < $ARTIFACT_REG_CRED
        - apk add openjdk17
    script:
        - ./gradlew bootBuildImage
        - docker tag sikepa:0.0.1-SNAPSHOT $IMAGE_REGISTRY/$IMAGE_TAG:stg-latest
        - docker push $IMAGE_REGISTRY/$IMAGE_TAG:stg-latest
    only:
        variables:
            - ($CI_COMMIT_BRANCH == "develop")
```

For other languages, it's still easy. You just need to write setup and build command on `Dockerfile` and run it using `docker build`.

After succesfully build and push the image, the application on server needs to be updated.
So the application is stopped, updated, and ran again to apply the changes.
Here's the example of it.

```
DeployStaging:
    stage: Deploy
    image: docker:latest
    before_script:
        - chmod 400 $SSH_PRIVATE_KEY
        - which ssh-agent || ( apk --update add openssh-client )
        - eval $(ssh-agent -s)
        - ssh-add $SSH_PRIVATE_KEY
        - mkdir -p ~/.ssh
        - chmod 700 ~/.ssh
        - cat $SSH_KNOWN_HOSTS >> ~/.ssh/known_hosts
        - chmod 644 ~/.ssh/known_hosts
        - docker login -u _json_key --password-stdin https://$IMAGE_REGISTRY < $ARTIFACT_REG_CRED
    script:
        - cat ~/.ssh/known_hosts
        - docker stop sikepa-backend || true
        - docker rm sikepa-backend || true
        - docker pull $IMAGE_REGISTRY/$IMAGE_TAG:stg-latest
        - docker run -p 127.0.0.1:8080:80 --env-file $PROD_ENV --name sikepa-backend -d $IMAGE_REGISTRY/$IMAGE_TAG:stg-latest
        - docker logs sikepa-backend
    variables:
        DOCKER_HOST: ssh://gitlab@$PROD_HOST
    only:
        variables:
            - ($CI_COMMIT_BRANCH == "develop")
```

Note: this job runs ssh to the server manually. There might be a more optimal way to run on automation.

This also could be scaled up so we could manage and run few services on just one instance without any security or interference issue.
(except if you misconfigure them, obviously)


### Docker Compose for Development

In local development, we might need to setup database or other softwares into our system. 
This could cause some interference if we have more than one project in our pc.
We could pull images from docker to run a database on a container.
But it might be hard to setup and manage the container.
In this case, docker compose is used to pull images, set the configuration, and run them as one network.

Here's the example of simple `docker-compose.yml` that pulls postgres and adminer and run them locally. 

```
version: "3.7"
services:
  postgres:
    container_name: postgres
    image: postgres:14
    ports:
      - "5432:5432"
    volumes:
      - ./docker_data/postgres_data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
  adminer:
    container_name: adminer
    image: adminer:latest
    environment:
      ADMINER_DEFAULT_SERVER: postgres
    ports:
      - 3645:8080
```

Save the file and run `docker-compose up -d`. Now you have your own database on a container.
To stop the container, use `docker-compose down`.

If you need to run other applications (such as RabbitMQ or Redis), you could just set the configuration and add the services
only on `docker-compose.yml`. It's really convenient.

### Conclusion

From this post, we learned that docker could be used as an automation tool to speed up development and deployment and make it easier to manage.

