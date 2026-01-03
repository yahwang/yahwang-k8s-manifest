https://github.com/acryldata/datahub-helm/tree/datahub-0.8.0

### datahub 유저 패스워드 확인

```
kubectl get secret dev-datahub-user-secret -n common -o jsonpath='{.data.user\.props}' | base64 --decode
```
