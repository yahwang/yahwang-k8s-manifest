https://github.com/acryldata/datahub-helm/tree/datahub-0.8.0

### datahub 유저 패스워드 확인

```
kubectl get secret dev-datahub-user-secret -n common -o jsonpath='{.data.user\.props}' | base64 --decode
```

### ingestion 설정

1. endpoint url을 ingress에 설정된 값으로 해야함

```
# nessie
uri: 'http://nessie.xxx.nip.io/iceberg'

# minio
s3.endpoint: 'http://minio-api.xxxx.nip.io'         
```

2. iceberg ingestion 설정

pyiceberg 최신버전 호환 안 되는 이슈가 있음

4번 Finish up - Advanced 설정에서 CLI 버전을 1.2.0.10으로 설정해야 함

### OIDC 설정

참고 : 이 두 설정 중 하나만 enabled해야 정상 동작함

```
- name: "AUTH_JAAS_ENABLED"
  value: "false"
- name: AUTH_OIDC_ENABLED
  value: "true"
```

설정을 바꿀 때마다 argocd application을 삭제하고 재생성해야 정상 동작함 ( 기존 데이터는 유지 )

OIDC 유저를 만들었다면 AUTH_JAAS_ENABLED인 변경해서 다시 admin으로 들어가 oidc user를 admin으로 변경해야 한다.
그 후 다시 OIDC로 변경하면 된다.