1. Clone the repo

git clone https://github.com/ATOAPaymentsLimited/SampleExpressApp



2. Dockerise the project create a docker file and docker-compose

Dockerfile
-----------
FROM node:16

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "index.js" ]

docker-compose.yaml
-------------------
version: "3"
services:
 apps:
       image: jaseel:1
       container_name: express_app
       restart: always
       ports:
       - "3000:3000"





3. Write a config file to deploy as a pod in Kubernetes with auto-scaling

kubectl create deployment expressapp --image=jaseel:1 --replicas=1 --dry-run=client -o yaml > deploy.yaml
kubectl apply -f deploy.yaml
kubectl autoscale deployment  expressapp    --cpu-percent=50 --min=1 --max=10 --dry-run=client -o yaml > autoscaling.yaml
kubectl apply -f autoscaling.yaml    
