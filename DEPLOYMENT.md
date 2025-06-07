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
   #### CHECK TEAMS ####
   

Authenticate docker with ghcr.io
1. Open browser
2. go to [dockerhub](https://app.docker.com/settings)
3. signin using github or google
4. Open terminal
    docker login -u rahulsingh
    #### CHECK TEAMS ####

Run the image after cicd pipeline has triggered and check the new image path in kubernetes/deployment.yml file
for locally running the docker ghcr image, use the following command
docker run -d -p 1010:80 ghcr.io/hellorahulsingh/devsecops-demo:sha-7e42235cd89cb27802e14e80b4e0eba897c486ff
http://localhost:1010/

if you are getting unaithorized issue for the above docker run command, follow this
```
Image visibility
If the image is private, then login is mandatory, and your GitHub user must have access to the repo that hosts the image.
To make the image public, go to:
GitHub > your repo > Packages > devsecops-demo > Package settings
→ Set visibility to public
```

if things are not working locally. then spin up a t2-medium instance on ec2 with the name argocd and use. ssh to access the server
```
chmod 400 ~/Documents/devsecops/rahul-argocd-setup.pem
sudo ssh -i ~/Documents/devsecops/rahul-argocd-setup.pem ubuntu@3.129.42.188
sudo apt update
sudo apt install docker.io -y
clear
sudo usermod -aG docker ubuntu
docker ps
exit
sudo ssh -i ~/Documents/devsecops/rahul-argocd-setup.pem ubuntu@3.129.42.188
docker ps
docker login -u rahulsingh
#### CHECK TEAMS ####
docker run -d -p 80:80 ghcr.io/hellorahulsingh/devsecops-demo:sha-7e42235cd89cb27802e14e80b4e0eba897c486ff
```