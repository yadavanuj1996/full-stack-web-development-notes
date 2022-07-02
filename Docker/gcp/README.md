## GCP


### To add dockeer iamge in GCR (Google Container Registry)
- To push images to your private registry hosted by gcr, you need to tag the images with a registry name. The format is [hostname]/[project-id]/[image]:[tag].
- For gcr:
  - [hostname]= gcr.io
  - [project-id]= your project's ID
  - [image]= your image name
  - [tag]= any string tag of your choice. If unspecified, it defaults to "latest".
- To fetch your project name 
  - gcloud config list project
- Tag docker image
  - docker tag node-app:0.2 gcr.io/[project-id]/node-app:0.2
- [hostname]/[project-id]/[image]:[tag]
- Push docker image
  - docker push gcr.io/[project-id]/node-app:0.2
- Pull docker image
  - docker pull gcr.io/[project-id]/node-app:0.2

