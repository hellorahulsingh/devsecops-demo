Build the docker image
docker build -t tiktactoe-demo:v1 .

Run docker image
docker run -d -p 9099:80 tiktactoe-demo:v1

===========================================

Github for container registry: https://ghcr.io [WE WILL BE USING THIS]
Docker for container registry: dockerhub
AWS for container registry: AWS ECR

Create access token in github, so that you can access ghcr.io using access token(check ci-cd.yml: line 101)
https://youtu.be/Ke_Wr5zPE0A?t=3279

Add the token generated above to your repo
1. go to repo
2. go to settings of the repo
3. left menu -> secrets and variabled -> actions
4. create new repository secret
4. fill the details
   TOKEN
   ####
   

Authenticate docker with ghcr.io
1. Open browser
2. go to [dockerhub](https://app.docker.com/settings)
3. signin using github or google
4. Open terminal
    docker login -u rahulsingh
    ####

