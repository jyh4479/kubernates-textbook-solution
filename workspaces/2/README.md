## 실습 과정에서 사용한 명령어 정리
    kubectl get pods -o custom-columns=NAME:metadata.name,LABELS:metadata.labels

    kubectl port-forward deploy/hello-kiamol-2 8080:80