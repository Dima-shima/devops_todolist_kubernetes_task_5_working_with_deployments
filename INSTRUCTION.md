kubectl apply -f .infrastructure/namespace.yml

kubectl apply -f .infrastructure/busybox.yml

kubectl apply -f .infrastructure/clusterIp.yml

kubectl apply -f .infrastructure/deployment.yml
strategy:
   type: RollingUpdate
   rollingUpdate:
     maxUnavailable: 1
     maxSurge: 1
resources:
        requests:
          cpu: 100m
          memory: 128Mi
        limits:
          cpu: 500m
          memory: 512Mi

kubectl apply -f .infrastructure/nodeport.yml

kubectl apply -f .infrastructure/hpa.yml
minReplicas: 2
 maxReplicas: 5
 metrics:
 - type: Resource
   resource:
     name: cpu
     target:
       type: Utilization
       averageUtilization: 70
 - type: Resource
   resource:
     name: memory
     target:
       type: Utilization
       averageUtilization: 70

kubectl config set-context --current --namespace=mateapp

kubectl get pods

kubectl get deployment

kubectl get replicaset

kubectl top node

kubectl get hpa