## 실습 과정에서 사용한 명령어 정리

### 실습 5.1.1

    kubectl apply -f sleep/sleep.yaml

    kubectl exec deploy/sleep -- sh -c 'echo ch05 > /file.txt; ls /*.txt'

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec -it deploy/sleep -- killall5

    kubectl get pod -l app=sleep -o jsonpath='{.items[0].status.containerStatuses[0].containerID}'

    kubectl exec deploy/sleep -- ls /*.txt
    