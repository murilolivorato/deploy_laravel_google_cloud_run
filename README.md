
# Deploying a Laravel Project on Google Cloud Run: A Step-by-Step Guide
This guide walks you through deploying a Laravel application on Google Cloud Run, covering everything from Docker configuration to setting up your project in the Google Cloud Console.

## Instructions -
https://medium.com/@murilolivorato/setting-up-a-laravel-development-environment-with-docker-and-docker-compose-a-step-by-step-5e37670ae640


## DEPLOY
# check region 
gcloud config list

# Look for the compute/region property in the output. If it is not set, you can set it using:
gcloud config set compute/region YOUR_REGION


# BUILD YOUR IMAGE TO TEST LOCAL

## CREATE TEST TAG
docker build -t laravel_gcr_deploy:test -f Dockerfile.prod .

## RUN TEST
docker run -p 8080:8080 laravel_gcr_deploy:test

# DEPLOY TO GCR
## TAG THE IMAGES FOR GCR
docker build -t gcr.io/YOUR_PROJECT_ID/laravel_gcr_deploy:v1.0.1 -f Dockerfile.prod .

## LIST IMAGE
docker images | grep laravel_gcr_deploy

## Push the images to GCR
docker push gcr.io/YOUR_PROJECT_ID/laravel_gcr_deploy:v1.0.1

Deploy to Google Cloud Run:
## Deploy the nginx service
gcloud run deploy laravel-deploy \
--image gcr.io/YOUR_PROJECT_ID/laravel_gcr_deploy:v1.0.1 \
--platform managed \
--region YOUR_REGION \
--allow-unauthenticated \
--set-env-vars "APP_ENV=production,APP_DEBUG=false,APP_KEY=base64:i454/GZWIz+PZ+yWn9Phce4YttD+SKR9V77zghd1Uds=,APP_URL=http://localhost,DB_CONNECTION=sqlite,SESSION_DRIVER=database,SESSION_LIFETIME=120,SESSION_ENCRYPT=false,SESSION_PATH=/,SESSION_DOMAIN=null,QUEUE_CONNECTION=database,CACHE_STORE=database,CACHE_PREFIX=,REDIS_CLIENT=phpredis,REDIS_HOST=127.0.0.1,REDIS_PASSWORD=null,REDIS_PORT=6379,MAIL_MAILER=log,MAIL_HOST=127.0.0.1,MAIL_PORT=2525,MAIL_USERNAME=null,MAIL_PASSWORD=null,MAIL_FROM_ADDRESS=hello@example.com,MAIL_FROM_NAME=Laravel"



Replace YOUR_PROJECT_ID, YOUR_REGION, and ENV_VAR_NAME=ENV_VAR_VALUE with your actual Google Cloud project ID, region, and environment variables.
Example Environment Variables

--set-env-vars "APP_ENV=production,APP_DEBUG=false,APP_KEY=base64:YOUR_APP_KEY"


if you like this code, give a like , enjoy 🚀 .