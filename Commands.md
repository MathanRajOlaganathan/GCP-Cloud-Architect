- gcloud app browse --version 20211214t182155
- gcloud app deploy --version v3 --no-promote
- gcloud app services set-traffic --splits=20211214t182155=.5, v3=.5 --split-by=random
- gcloud app deploy
- gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project gke-cockroach
- kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
- kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
- kubectl scale deployment hello-world-rest-api --replicas=4
- gcloud container clusters resize cluster-1 --node-pool default-pool --num-nodes 4 --zone us-central1-c
- kubectl autoscale deployment hello-world-rest-api --max=4 --cpu-percent=10
- kubectl get hpa
- gcloud container clusters update cluster-1 --enable-autoscaling --min-nodes=1 --max-nodes=5 --zone=us-central1-c
- kubectl create configmap heelo-world-config --from-literal=DB_NAME=customer
- kubectl get configmap
- kubectl describe configmap heelo-world-config
- kubectl create secret generic hello-world-secret --from-literal=DB_PASSWORD=mass
- kubectl describe secret hello-world-secret
- gcloud container node-pools list --cluster=cluster-1 --zone=us-central1-c
- kubectl delete service hello-world-rest-api
- kubectl delete deployment hello-world-rest-api
- gcloud container clusters delete cluster-1 --zone=us-central1-c
- gcloud container clusters delete
- kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE
- kubectl get pods
- kubectl get replicasets
- gcloud run deploy first-service --image image_url --revision-suffix v1
- gcloud run revisions list
- gcloud run services update-traffic myservice --to-revisions=v2=10,v1=90
- gcloud compute project-info describe
- gcloud auth list 
- gcloud projects get-iam-policy glowing-furnace-304608
- gcloud projects add-iam-policy-binding glowing-furnace-304608 --member=user:in28minutes@gmail.com --role=roles/storage.objectAdmin
- gcloud projects remove-iam-policy-binding glowing-furnace-304608 --member=user:in28minutes@gmail.com --role=roles/storage.objectAdmin
- gcloud iam roles describe roles/storage.objectAdmin
- gcloud iam roles copy --source=roles/storage.objectAdmin 
- gcloud sql connect my-sql --user=root --quiet  