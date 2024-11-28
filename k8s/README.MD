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


查看POD的yaml文件（确认使用了istio-proxy）
kubectl get pod <pod-name> -o yaml

测试网关的pod
kubectl get pods -l app=gateway -o wide
curl http://10.244.2.9:10000/api/service-a/version
这里会负载两个不同的service-a的版本v1和v2
curl http://10.244.2.9:10000/api/service-a/trace

定义版本：
kubectl apply -f destination-rule-all.yaml
配置默认路由-路由到v2
kubectl apply -f virtual-service-all-v2.yaml
再次测试：curl http://10.244.2.9:10000/api/service-a/version 都是路由到版本v2


定义前端网关：
kubectl apply -f frontend-gateway.yaml
确认网关：
kubectl get gateway

重新更新(由于已经设置了 imagePullPolicy: Always，重启时会自动拉取最新镜像)：
kubectl rollout restart deployment/service-a-v1
kubectl rollout restart deployment/service-a-v2
kubectl rollout restart deployment/frontend-react-v1
kubectl rollout restart deployment/frontend-react-v2
