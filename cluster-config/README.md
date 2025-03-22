# apps

## 1. harbor

https://github.com/goharbor/harbor-helm/tree/v1.15.2

### 1-1. harbor keycloak 연동하는 법

https://velog.io/@lijahong/0%EB%B6%80%ED%84%B0-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-Keycloak-%EA%B3%B5%EB%B6%80-OIDC%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-Keycloak-Harbor-SSO-%EC%97%B0%EB%8F%99

### 1-2. harbor registry 등록하는 법

```
kubectl create secret docker-registry harbor-registry \
    --namespace common \
    --docker-server=https://harbor.yahwang.site \
    --docker-username=your-username \
    --docker-password=your-password
```

robot account의 경우 robot\$이름 ( \$를 써야 한다. )

## 2. ingress-nginx

https://github.com/kubernetes/ingress-nginx/tree/helm-chart-4.11.3/charts/ingress-nginx

## 3. redis

https://github.com/bitnami/charts/tree/redis/20.6.0/bitnami/redis

## 4. keycloak

https://github.com/bitnami/charts/tree/keycloak/24.2.2/bitnami/keycloak

### 4-1. github 연동하는 법

https://www.youtube.com/watch?v=_72InRW4bdU&t=215s

## 5. jenkins

https://github.com/jenkinsci/helm-charts/tree/jenkins-5.7.24/charts/jenkins

### 5-1. keycloak 연동하는 법

https://docs.google.com/document/d/1gmHjU0YAAtLIS9nit9JSXdj43NoickEHa1rEmAoqz3E/edit?usp=sharing

## 6. cert-manager

https://github.com/cert-manager/cert-manager/blob/v1.16.2/deploy/charts/cert-manager/values.yaml

### 6-1. Let's Encrypt와 NGINX Ingress Controller 활용

https://hbayraktar.medium.com/installing-cert-manager-and-nginx-ingress-with-lets-encrypt-on-kubernetes-fe0dff4b1924

cluster-issuer는 namespace와 관계없음

```
kubectl apply -f cluster-issuer.yaml
```

### 6-2. Ingress 설정

cert-manager.io/cluster-issuer: issuer에서 설정한 이름

tls secretName: 이름만 설정 시 자동으로 생성됨

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - my-domain
    secretName: my-domain-tls
  rules:
  - host: my-domain
```

## 7. grafana

https://github.com/grafana/helm-charts/tree/grafana-8.8.2/charts/grafana

## 8. loki

https://github.com/grafana/loki/tree/v3.3.2/production/helm/loki

https://grafana.com/docs/loki/latest/operations/storage/retention/#configuring-the-retention-period

## 9. prometheus

kube-prometheus-stack으로 설치하여 POD monitor, server, operator 등 한 번에 설치

https://github.com/prometheus-community/helm-charts/tree/kube-prometheus-stack-67.10.0/charts/kube-prometheus-stack


## 10. sealed-secrets

https://github.com/bitnami-labs/sealed-secrets/tree/v0.28.0

참고: kubeseal도 별도로 설치해야 함

### 10-1. sealed-secret 생성 방법

--controller-name: sealed-secrets service name

--controller-namespace: sealed-secrets namespace (default: kube-system) 생략 가능

```
# 기존 secret으로 yaml 만드는 법

kubectl get secret minio-secret -n common -o yaml | kubeseal --controller-name dev-sealed-secrets --scope namespace-wide -w mysealedsecret.yaml -o yaml

# sealed secret 암호화 검증 ( 아무 결과가 없으면 정상 )

kubeseal --controller-name dev-sealed-secrets -f mysealedsecret.yaml --validate
```


# operators

## 1. vector-operator

https://github.com/kaasops/vector-operator/tree/main/helm/charts/vector-operator

## 2. eck-operator

https://github.com/elastic/cloud-on-k8s/tree/v2.14.0/deploy/eck-operator

## 3. strimzi-kafka-operator

https://github.com/strimzi/strimzi-kafka-operator/tree/0.43.0/helm-charts/helm3/strimzi-kafka-operator

## 4. minio-operator

https://github.com/minio/operator/tree/v6.0.2/helm/operator