# 민감 정보 검열 처리한 Backend_Manifests 파일입니다.
## 사용법
* argocd에 본 리포지토리를 등록한다.
* 아래와 같이 yaml 파일을 만든다.
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: backend-(각 폴더 이름)
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/LG-CNS-2-FINAL-PROJECT-FINANCE/Backend_Manifests.git
    targetRevision: master
    path: (각 폴더 이름)
    helm:
      valueFiles:
        - values-dev.yaml
  destination:
    server: https://kubernetes.default.svc
    namespace: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```
* kubectl apply -f를 해서 배포한다!
* 변수값 변경이 필요할 때는, values-dev/prod.yaml 값을 변경하고, 변수 추가가 필요하면 values-*.yaml뿐만 아닌 templates 폴더에 해당되는 곳(configmap,secret 등)에도 추가가 필요하다.
 * 단, values-*.yaml의 키는 하이픈(-)이 먹히지 않기 때문에 카멜 케이스로 작성한다.
