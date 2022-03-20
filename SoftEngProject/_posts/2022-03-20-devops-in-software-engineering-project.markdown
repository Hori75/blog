---
layout: post
title:  "DevOps on Software Engineering Project"
author: hori75
date:   2022-03-20 15:42:00 +0700
background: '/images/grafana.png'
excerpt_separator: <!--more-->
---

Quick pace development demands quick deployment and delivery of the products.
<!--more-->
Nowadays, changes in the application makes deployment needed to be done in automated and quick manner.
This has to be done in order to fulfill the demand on time.
Here's my grasp on automating the deployment and integration process.

### Overview of DevOps

Usually, DevOps represents a collaboration between the Development and Operation process in order to deploy code
 into production environment. This collaboration dedicates on creating an automated and fast way to deploy the code.
DevOps is important for enterprises that needs to deliver product faster to be competitive.
This demands a collaboration between development, operations, and business teams so the development could be done 
in timely manner.

In practice, DevOps includes some common practices done and its examples.

#### Collaborative Development

![Gitlab Page](/images/gitlab-page.png){: width="800" }

In order to develop product quickly, we should enable other team member to work pararelly.
This is usually done by using a remote host to store source code and version control system.

The most common example here is using popular code hosting platform such as [Github](https://github.com), 
[BitBucket](https://bitbucket.org), [Gitlab](https://gitlab.com), etc.
You could host your own code hosting platform (for example, [host Gitlab on your own server](https://about.gitlab.com/install/))
but it might costs too much in the early development. 
The code hosting platform should be operational and reliable to maintain, 
so you could have used available hosting platform instead.


#### Continuous Integration and Deployment

![Continuous Integration and Deployment](/images/pipeline.png){: width="800" }

This is where DevOps dedicated most. 
During the integration process, the source code should be built and tested before deployed to production.
Due to high volume of work done from the development, the process should be done in automated way.

Usually, the automation is available on code hosting platform as a feature.
Also, there are many services that provide automation platform, such as [Travis CI](https://travis-ci.org), 
[Circle CI](https://circleci.com), etc.
But, it might be limited due to be demanding in terms of computational cost and enermous amount of jobs need to be done pararelly.
You could use either free in limited way or find the cheapest and most reliable.
The other way is to host your own CI/CD runner like [Gitlab Runner](https://docs.gitlab.com/runner/)
provided for Gitlab servers or [Jenkins](https://www.jenkins.io/).

As for deployment, there are many Platform as a Service (PaaS) services that provide platform to be manage by ourselves.
The example of it are [Heroku](https://www.heroku.com/), [Digital Ocean](https://www.digitalocean.com/), 
[Google Cloud Platform](https://cloud.google.com), etc. You could utilize any platform as you like.
Take note that there are few things needed to setup in order to make a fully operational web application, 
such as, setting up how the application runs or replaced by the newer build.

#### Continuous Monitoring

![Monitoring](/images/grafana.png){: width="800" }

After deployment to production, we should check if the server works properly and could fulfill the demand.
We also need to check what happened on the service when something wrong happened.
This is what app logs are used for, but you need to be able to read it easily,
especially when you already have many servers operational.
The problem also apply on checking performances on the servers.

The tools you can use are [Grafana](https://grafana.com/), [Prometheus](https://prometheus.io/), etc.
The monitoring tools should be able to provide access to performance graph, app logs, and alerts.  


### Conclusion

DevOps has become the important part on software engineering projects. 
It happens due to the increase of competitive companies that needs to deliver product in time.
This also make software development and deployment more easier and faster.
But we should remember, the team needs to be adaptive in order to be able to adopt DevOps practices in beneficial way.
