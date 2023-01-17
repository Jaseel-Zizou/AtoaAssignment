1. Clone the repo

git clone https://github.com/ATOAPaymentsLimited/SampleExpressApp



2. Dockerise the project create a docker file and docker-compose

Find the Dockerfile in the repo,
Find the docker-compose.yaml  in the repo


3. Write a config file to deploy as a pod in Kubernetes with auto-scaling

kubectl create deployment expressapp --image=jaseel:1 --replicas=1 --dry-run=client -o yaml > deploy.yaml

kubectl apply -f deploy.yaml

kubectl autoscale deployment  expressapp    --cpu-percent=50 --min=1 --max=10 --dry-run=client -o yaml > autoscaling.yaml

kubectl apply -f autoscaling.yaml    
