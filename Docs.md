Contenerize an API and Which will Run on K8s

1- Run your code a make sure it's working


2- On  GitHub
  Create a repository "myrepo"
  Copy the code into "myrepo" using an editor


3- LINUX TERMINAL OR GITBASH
   mkdir "myrepo"
   cd "myrepo"
   git init
   git remote add origin "url ofyour new repository in github"
   echo "#README" >> README.md
   tar -czvf "name newfilecode.tar.gz oldfilecode
   git status
   git add .
   git commit -m "New Code"
   git push origin -u "branch name"


4- Create a Dockerfile
   touch Dockerfile
   vim Dockerfile
   FROM
   MAINTAINER
   RUN mkdir -p "path of the Directory"
   RUN apt install git -y
   RUN git clone "Path of your git repository"
   ENV
   EXPOSE 
   CMD
   :wq


5- Build and push your Images  Docker
   docker login
   docker build -t "nameofApp" .
   docker images
   docker push "ImagesID"

SETUP your Kubernetes Environment


6- Create a yaml files for your pods deployment
   touch "my-app.yml"
   vim "my-app.yml"

apiVersion: apps/v1 
kind: Deployment
metadata:
  name: my-app
spec:
  selector:
    matchLabels:
      app: my-app
  replicas: 1 
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1

  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: "dockerrepo/appname
        imagePullPolicy: Always
        ports:
        - containerPort: 
 
kubectl create -f "my-app.yml"


7- Create an Internal service
   
     touch "my-app-internal-service.yml"
     vim "my-app-internal-service.yml"

apiVersion: v1
kind: Service
metadata:
  name: my-app-internal-service
  labels:
    app: my-app
spec:
  selector:
    app: my-app
  type: LoadBalancer
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
      nodePort: 
:wq

kubectl create -f "my-app-internal-service.yml"


6- Install your Ingress controller in minikube
   minikube addons enable ingress


7- Create an ingress roles to expose our deployment externally

  kubectl get all -n kubernetes-dashbord 
To check all the pods and services created
  
  touch "my-app-ingress.yml"
  vim "my-app-ingress.yml"

apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: my-app-ingress
  namespace: kubernetes-my-app
spec:
  rules:
  - hosts: my-app.com
    http:
      paths:
      - backend:
           serviceName: kubernetes-my-app
           servicePort: 

kubectl apply or create -f "my-app-ingress.yml"


8- Setup the Hosts files in K8s

   kubectl get ingress -n kubernetes-my-app
to get the Ip address of the of the pods 0.0.0.0
 
vim /etc/hosts
paste the IP address at the end of your file to map it to your domain name created
0.0.0.0       my-app.com
:wq


