## 실습 과정에서 사용한 명령어 정리
    kubectl run hello-kiamol --image=kiamol/ch02-hello-kiamol

    kubectl create deployment hello-kiamol-2 --image=kiamol/ch02-hello-kiamol

    kubectl get pods -o custom-columns=NAME:metadata.name,LABELS:metadata.labels

    kubectl port-forward deploy/hello-kiamol-2 8080:80

    kubectl get pods -o custom-columns=NAME:metadata.name,POD_IP:status.podIP
    
    kubectl exec -it hello-kiamol sh
        - hostname -i
        - wget -O - http://localhost | head -n 4
        - exit

    kubectl logs --tail=2 hello-kiamol

    kubectl exec deploy/hello-kiamol-4 -- sh -c 'wget -O - http://localhost > /dev/null'

    kubectl logs --tail=1 -l app=hello-kiamol-4

## 파드 속 파일 시스템 접근 실습
    mkdir -p /tmp/kiamol/ch02
    kubectl cp hello-kiamol:/usr/share/nginx/html/index.html /tmp/kiamol/ch02/index.html
    cat /tmp/kiamol/ch02/index.html

## 파드 삭제에 대한 내용
    kubectl delete pods --all
        - 하지만 기존 deployment가 남아있어 pods들이 다시 생성되는 경우가 있음
    
    kubectl delete deploy --all