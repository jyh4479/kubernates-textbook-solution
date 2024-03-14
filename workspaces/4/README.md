## 실습 과정에서 사용한 명령어 정리

### 실습 4.1.1

    kubectl apply -f sleep/sleep.yaml

    kubectl wait --for=condition=Ready pod -l app=sleep

    kubectl exec deploy/sleep -- printenv HOSTNAME KIAMOL_CHAPTER

### 실습 4.1.2

    kubectl apply -f sleep/sleep-with-env.yaml

    kubectl exec deploy/sleep -- printenv HOSTNAME KIAMOL_CHAPTER

### 실습 4.1.3

    kubectl create configmap sleep-config-literal --from-literal=kiamol.section='4.1'

    kubectl get cm sleep-config-literal

    kubectl describe cm sleep-config-literal

    kubectl apply -f sleep/sleep-with-configMap-env.yaml

    kubectl exec deploy/sleep -- sh -c 'printenv | grep "KIAMOL"'

### 실습 4.2.1

    kubectl create configmap sleep-config-env-file --from-env-file=sleep/ch04.env

    kubectl get cm sleep-config-env-file

    kubectl apply -f sleep/sleep-with-configMap-env-file.yaml

    kubectl exec deploy/sleep -- sh -c 'printenv | grep "^KIAMOL"'

### 실습 4.2.2

    kubectl apply -f todo-list/todo-web.yaml

    kubectl wait --for=condition=Ready pod -l app=todo-web

    kubectl get svc todo-web -o jsonpath='http://{.status.loadBalancer.ingress[0].*:8080}'

    kubectl logs -l app=todo-web

### 실습 4.2.3
    
    kubectl apply -f todo-list/configMaps/todo-web-config-dev.yaml

    kubectl apply -f todo-list/todo-web-dev.yaml

### 실습 4.3.1

    kubectl exec deploy/todo-web -- sh -c 'ls -l /app/app*.json'

    kubectl exec deploy/todo-web -- sh -c 'ls -l /app/config/*.json'

    kubectl exec deploy/todo-web -- sh -c 'echo ch04 >> /app/config/config.json'

### 실습 4.3.2

    kubectl logs -l app=todo-web

    kubectl apply -f todo-list/configMaps/todo-web-config-dev-with-logging.yaml

    sleep 120

    kubectl exec deploy/todo-web -- sh -c 'ls -l /app/config/*.json'

    kubectl logs -l app=todo-web

### 실습 4.3.3

    kubectl apply -f todo-list/todo-web-dev-broken.yaml

    kubectl logs -l app=todo-web

    kubectl get pods -l app=todo-web

### 실습 4.3.4
    
    kubectl apply -f todo-list/todo-web-dev-no-logging.yaml

    kubectl exec deploy/todo-web -- sh -c 'ls /app/config'

    kubectl get logs -l app=todo-web

    kubectl get pods -l app=todo-web