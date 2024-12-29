## vector-operator

https://github.com/kaasops/vector-operator/tree/main/helm/charts/vector-operator

## eck-operator

https://github.com/elastic/cloud-on-k8s/tree/v2.14.0/deploy/eck-operator

## strimzi-kafka-operator

https://github.com/strimzi/strimzi-kafka-operator/tree/0.43.0/helm-charts/helm3/strimzi-kafka-operator

## minio-operator

https://github.com/minio/operator/tree/v6.0.2/helm/operator

## harbor

https://github.com/goharbor/harbor-helm/tree/v1.15.2

### harbor keycloak 연동하는 법

https://velog.io/@lijahong/0%EB%B6%80%ED%84%B0-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-Keycloak-%EA%B3%B5%EB%B6%80-OIDC%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-Keycloak-Harbor-SSO-%EC%97%B0%EB%8F%99

### harbor registry 등록하는 법

```
kubectl create secret docker-registry harbor-registry \
    --namespace common \
    --docker-server=https://harbor.yahwang.site \
    --docker-username=your-username \
    --docker-password=your-password \
```

## ingress-nginx

https://github.com/kubernetes/ingress-nginx/tree/helm-chart-4.11.3/charts/ingress-nginx

## redis

https://github.com/bitnami/charts/tree/redis/20.6.0/bitnami/redis

## keycloak

https://github.com/bitnami/charts/tree/keycloak/24.2.2/bitnami/keycloak

### github 연동하는 법

https://www.youtube.com/watch?v=_72InRW4bdU&t=215s

## jenkins

https://github.com/jenkinsci/helm-charts/tree/jenkins-5.7.24/charts/jenkins

### keycloak 연동하는 법

https://docs.google.com/document/d/1gmHjU0YAAtLIS9nit9JSXdj43NoickEHa1rEmAoqz3E/edit?usp=sharing

## cert-manager

https://github.com/cert-manager/cert-manager/blob/v1.16.2/deploy/charts/cert-manager/values.yaml

### Let's Encrypt와 NGINX Ingress Controller 활용

https://hbayraktar.medium.com/installing-cert-manager-and-nginx-ingress-with-lets-encrypt-on-kubernetes-fe0dff4b1924

cluster-issuer는 namespace와 관계없음

```
kubectl apply -f cluster-issuer.yaml
```

### Ingress 설정

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
