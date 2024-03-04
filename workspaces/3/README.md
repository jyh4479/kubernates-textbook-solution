## 실습 과정에서 사용한 명령어 정리

### 실습1
    kubectl apply -f sleep/sleep1.yaml -f sleep/sleep2.yaml

    kubectl wait --for=condition=Ready pod -l app=sleep-2

    kubectl exec deploy/sleep-1 -- ping -c 2 $(kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}')

### 실습2
    kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}' 

    kubectl delete pods -l app=sleep-2

    kubectl get pod -l app=sleep-2 --output jsonpath='{.items[0].status.podIP}' 

### 실습3
    kubectl apply -f sleep/sleep2-service.yaml

    kubectl get svc sleep-2
    
    kubectl exec deploy/sleep-1 -- ping -c 1 sleep-2

    (해당 실습을 진행하면서 ping이 되지 않은 이유 다시 확인해보기 서비스가 뭔지도 봐야할듯)

### 실습4
    

