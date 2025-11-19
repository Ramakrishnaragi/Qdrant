# Qdrant Kubernetes Deployment Task

## Task Description
Deploy a Qdrant cluster on Kubernetes with the following specifications:

- 1 master node (read-write)
- 2 replica nodes (read-only)
- Pods configured with appropriate environment variables
- Cluster should be verifiable through API and pod status

---

## Folder Structure
qdrant-k8s-task/
├── README.md
├── qdrant-configmap.yaml # Configuration for Qdrant
├── qdrant-headless-svc.yaml # Headless service for StatefulSet
├── qdrant-lb.yaml # LoadBalancer for read-only replicas
├── qdrant-read.yaml # Read-only replica deployment/config
├── qdrant-service.yaml # Service for master
├── qdrant-statefulset.yaml # StatefulSet for master and replicas
├── qdrant-write-lb.yaml # LoadBalancer for master node
└── qdrant-write.yaml # Master node deployment/config
└── screenshots/



---

## Setup Instructions

1. **Apply ConfigMap**
```bash
kubectl apply -f kubernetes/qdrant-configmap.yaml
2. **Deploy Headless Service**
kubectl apply -f kubernetes/qdrant-headless-svc.yaml
3. **Deploy Master Node**
kubectl apply -f kubernetes/qdrant-write.yaml
4. **Deploy Read-Only Replicas**
kubectl apply -f kubernetes/qdrant-read.yaml
5. **Deploy LoadBalancers**
kubectl apply -f kubernetes/qdrant-write-lb.yaml
kubectl apply -f kubernetes/qdrant-lb.yaml
6. **Deploy StatefulSet**
kubectl apply -f kubernetes/qdrant-statefulset.yaml
7. **Deploy General Service**
kubectl apply -f kubernetes/qdrant-service.yaml
Verify Deployment
   Check Pods:
      kubectl get pods -n qdrant
   Check Services:
      kubectl get svc -n qdrant
    Test Qdrant API:
      curl -X GET <service-ip>:6333/collections -H "api-key: <your-api-key>"

!<img width="1037" height="73" alt="image" src="https://github.com/user-attachments/assets/978e66da-8a01-4a95-915f-6f10cf8f0fdd" />

!<img width="1877" height="122" alt="image" src="https://github.com/user-attachments/assets/5872dd00-9afb-4aa4-a719-229e66f33243" />

!<img width="1882" height="166" alt="image" src="https://github.com/user-attachments/assets/36108d6a-9d86-4d80-a259-b454025208f5" />

!<img width="1503" height="783" alt="image" src="https://github.com/user-attachments/assets/7b2cf81b-5e4e-4467-9589-59842bb0f872" />



Notes

Environment variable QDRANT__CONSENSUS__PEERS is configured in StatefulSet YAML to define master and replica nodes.

Master node is read-write, replicas are read-only.

Headless service is used for internal pod communication.


