## Create the Docker Image

Follow the steps in `StepsToPushToGCR.txt` to create and push the Docker image to Google Cloud Registry.

## Create the Kubernetes Deployment

1. Apply the deployment configuration using the command:

kubectl apply -f createDeployment.yaml

2. Verify the deployment using the command:

kubectl get pods

## Create the Kubernetes Service
1. Apply the service configuration using the command:

kubectl apply -f createService.yaml

2. Check the URL using port 8037 on localhost.

The createService.yaml file contains the following configuration:
apiVersion: v1
kind: Service
metadata:
  name: example-service
spec:
  selector:
    tier: frontend
  clusterIP: 10.99.132.220
  externalTrafficPolicy: Cluster
  ports:
  - name: myport
    port: 8037
    protocol: TCP
    targetPort: 3040
  type: LoadBalancer

  In this configuration, the service named example-service is created. It targets pods with the label tier: frontend. It exposes port 8037 and forwards traffic to port 3040 of the pods. The type of the service is LoadBalancer, which means it will be accessible through a public IP address.