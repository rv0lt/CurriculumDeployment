# CurriculumDeployment


This project consists of a deployment of a nginx application built on Docker that serves on localhost:8080/cv my resume. It makes use of a Scratch image for a safer enviroment.

# 

This is a demo project just for fun and to learn, the origin of the idea and the full process of creating it is available on my [blog](https://rv0lt.github.io/2023/03/21/distroless-scratch-dockerifles.html).

#

With GitHub actions, everytime I modify my resume, it will built again the pdf and push the image to the dockerhub registry. The kube folder contains a yaml file to deploy it in a Kubernetes Clusters as well as a Helm chart to deploy it using helm!

You can use the public docker Hub image to deploy this service [link](https://hub.docker.com/repository/docker/rv0lt/mycv/general).
