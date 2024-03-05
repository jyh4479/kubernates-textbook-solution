## 실습 과정에서 사용한 명령어 정리

### 실습 3.1.1

    kubectl apply -f sleep/sleep1.yaml -f sleep/sleep2.yaml

    kubectl wait --for=condition=Ready pod -l app=sleep-2

    kubectl exec deploy/sleep-1 -- ping -c 2 $(kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}')

### 실습 3.1.2

    kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}' 

    kubectl delete pods -l app=sleep-2

    kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}' 

### 실습 3.1.3

    kubectl apply -f sleep/sleep2-service.yaml

    kubectl get svc sleep-2
    
    kubectl exec deploy/sleep-1 -- ping -c 1 sleep-2

    (해당 실습을 진행하면서 ping이 되지 않은 이유 다시 확인해보기 서비스가 뭔지도 봐야할듯)

### 실습 3.2.1

    kubectl apply -f numbers/api.yaml -f numbers/web.yaml

    kubectl wait --for=condition=Ready pod -l app=numbers-web

    kubectl port-forward deploy/numbers-web 8080:80

### 실습 3.2.2

    kubectl apply -f numbers/api-service.yaml

    kubectl get svc numbers-api

    kubectl port-forward deploy/numbers-web 8080:80

    (실습 4 에서의 문제를 실습 5에서 해소)

### 실습 3.2.3

    kubectl get pod -l app=numbers-api -o custom-columns=LABELS:metadata.labels,POD_ID:status.podIP

    kubectl delete pod -l app=numbers-api

    kubectl get pod -l app=numbers-api -o custom-columns=LABELS:metadata.labels,POD_ID:status.podIP

    kubectl port-forward deploy/numbers-web 8080:80

### 실습 3.3.1

    kubectl apply -f numbers/web-service.yaml

    kubectl get svc numbers-web

    kubectl get svc numbers-web -o jsonpath='http://{.status.loadBalancer.ingress[0].*}:8080'

#### minikube에서 external ip <pending> 문제

    external ip를 제공하는 AWS, Azure, GCP등 에서 사용하는 경우는 문제 X
    minikube등 로컬 환경에서 사용시 문제가 되는데 별도의 터미널을 열어서 minikube tunnel 명령을 사용하면 해결된다.
    
    TODO: 위와 같이 실했을때 왜 실행되는지 확인해보기