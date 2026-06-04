


backend/
 ├── package.json
 ├── server.js
 └── Dockerfile


npm init -y
npm install express


After creation of docker file

docker build -t backend:v1 .

where docker

set PATH=%PATH%;C:\Program Files\Docker\Docker\resources\bin


docker build -t backend:v1 .     --> Docker Image backend:v1

![alt text](image.png)

Your PC
└── Docker Engine
    └── Images
        └── backend:v1

docker run -p 5000:5000 backend:v1

This command:

Took the image backend:v1
Created a container from it
Started the container

Dockerfile
    ↓ build
Image (backend:v1)
    ↓ run
Container


docker build -t frontend:v1 .


docker run -p 5173:5173 frontend:v1  -->Exact port need to be replicated 



minikube start

Get Nodes :

kubectl get nodes

minikube image load backend:v1

minikube image load frontend:v1

kubectl get svc


kubectl describe svc frontend-service

minikube service list


kubectl logs deployment/frontend


kubectl exec -it frontend-5b75d5c66f-rk78m -- netstat -tulpn


kubectl exec -it frontend-5b75d5c66f-rk78m -- ss -tulpn


kubectl port-forward svc/frontend-service 5173:5173



C:\Users\amit\Documents\GitHub\Docker-Syntax\Docker\Full dock\frontend>kubectl get pods
NAME                        READY   STATUS    RESTARTS   AGE
backend-5d7b6c5c44-gkhw9    1/1     Running   0          24m
backend-5d7b6c5c44-svs85    1/1     Running   0          24m
frontend-5b75d5c66f-rk78m   1/1     Running   0          18m
frontend-5b75d5c66f-vxsmd   1/1     Running   0          18m

C:\Users\amit\Documents\GitHub\Docker-Syntax\Docker\Full dock\frontend>kubectl delete pod backend-5d7b6c5c44-gkhw9
pod "backend-5d7b6c5c44-gkhw9" deleted from default namespace


Had deleted pod now it will create a new Pod 

C:\Users\amit\Documents\GitHub\Docker-Syntax\Docker\Full dock\frontend>kubectl get pods -w
NAME                        READY   STATUS    RESTARTS   AGE
backend-5d7b6c5c44-cwxbf    1/1     Running   0          40m
backend-5d7b6c5c44-svs85    1/1     Running   0          65m
frontend-5b75d5c66f-rk78m   1/1     Running   0          59m
frontend-5b75d5c66f-vxsmd   1/1     Running   0          59m



kubectl scale deployment backend --replicas=5

You ran:

kubectl scale deployment backend --replicas=5

Output:

deployment.apps/backend scaled

means Kubernetes accepted the request.

Before scaling

You had something like:

backend-5d7b6c5c44-gkhw9
backend-5d7b6c5c44-svs85

which is 2 backend pods.

After scaling

Kubernetes will create 3 additional backend pods so that there are 5 total:

backend-xxxxx-abcde
backend-xxxxx-fghij
backend-xxxxx-klmno
backend-xxxxx-pqrst
backend-xxxxx-uvwxy
Verify it

Run:

kubectl get pods

You should see 5 backend pods.


kubectl get deployments

kubectl get pods



General FLow 

Cluster
│
└── Node (minikube)
      │
      ├── Deployment: frontend
      │      │
      │      ▼
      │   ReplicaSet
      │      │
      │      ▼
      │   Frontend Pods
      │      │
      │      ▼
      │   Containers
      │
      ├── Deployment: backend
      │      │
      │      ▼
      │   ReplicaSet
      │      │
      │      ▼
      │   Backend Pods
      │      │
      │      ▼
      │   Containers
      │
      ├── frontend-service
      └── backend-service

      Deployment → defines desired state.
ReplicaSet → maintains replica count.
Pod → runs containers.
Service → provides stable networking and load balancing.
Probes → health checks.
Scheduler → places pods on nodes.
Self-healing → replaces failed pods automatically.
Scaling → increases/decreases pod count on demand.



Cluster
 └── Node 1
      ├── Frontend Pod
      ├── Frontend Pod
      ├── Backend Pod
      └── Backend Pod



Cluster
│
├── Node 1
│    ├── Frontend Pod
│    └── Backend Pod
│
└── Node 2
     ├── Frontend Pod
     └── Backend Pod