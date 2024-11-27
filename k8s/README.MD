kubectl apply -f demo.yaml

测试service-b的pod
kubectl get pods -l app=service-b -o wide
curl http://<pod-xxx-ip>:10002/api/cost

测试service-a的pod
kubectl get pods -l app=service-a -o wide
curl http://<pod-xxx-ip>:10001/service-a/version


测试service-a的svc
kubectl port-forward svc/service-a 10001:10001
curl http://localhost:10001/service-a/version

测试service-b的svc
kubectl port-forward svc/service-b 10002:10002
curl http://localhost:10002/api/cost




