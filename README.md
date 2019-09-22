# laravel-on-fargate
Laravel App on AWS Fargate Demo

## laravel-app
A simple Laravel app based on laravel demo application.

## nginx-web
A simple nginx image with some modification.

# Prequisites
You need to have:
- Docker installed
- AWS Account

*Disclaimer: Deploying on Fargate will incur charges for your AWS account.*

# Step-by-step Tutorial

1. Build images for both laravel-app and nginx-web.
2. Push the images to your ECR repositories.
3. Create a Fargate cluster.
4. Write a TaskDefinition:
  - Make sure to include both images in Containers Definition.
  - Also create a shared Volume and mount at "/var/www".
5. Finally, you can either run the Task or create a Service to make sure your app keep running.

For more detailed information you can read the article here: https://medium.com/@yosi.pramajaya/multi-containers-app-on-aws-fargate-e86d9dc6e207
