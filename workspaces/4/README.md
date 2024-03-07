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