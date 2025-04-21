https://github.com/acryldata/datahub-helm/tree/datahub-0.5.13

### datahub 유저 패스워드 확인

```
kubectl get secret dev-datahub-user-secret -n common -o jsonpath='{.data.user\.props}' | base64 --decode
```
