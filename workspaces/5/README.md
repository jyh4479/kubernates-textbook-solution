## 실습 과정에서 사용한 명령어 정리

### 실습 5.1.1

    kubectl apply -f sleep/sleep.yaml

    kubectl exec deploy/sleep -- sh -c 'echo ch05 > /file.txt; ls /*.txt'

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec -it deploy/sleep -- killall5

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec deploy/sleep -- ls /*.txt

### 실습 5.1.2
    
    kubectl apply -f sleep/sleep-with-emptyDir.yaml

    kubectl exec deploy/sleep -- ls /data

    kubectl exec deploy/sleep -- sh -c 'echo ch05 > /data/file.txt; ls /data'

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec deploy/sleep -- killall5

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec deploy/sleep -- cat /data/file.txt

### 실습 5.2.1

    kubectl apply -f pi/v1/

    kubectl wait --for=condition=Ready pod -l app=pi-web

    kubectl get svc pi-proxy -o jsonpath='http://{.status.loadBalancer.ingress[0].*}:8080/?dp=30000'

    kubectl exec deploy/pi-proxy -- ls -l /data/nginx/cache

### 실습 5.2.2

    kubectl delete pod -l app=pi-proxy

    kubectl exec deploy/pi-proxy -- ls -l /data/nginx/cache


    