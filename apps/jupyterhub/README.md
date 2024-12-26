### values.yaml

https://github.com/jupyterhub/zero-to-jupyterhub-k8s/tree/4.0.0/jupyterhub

### keycloak oidc 연동

https://github.com/jupyterhub/zero-to-jupyterhub-k8s/blob/4.0.0/docs/source/administrator/authentication.md#keycloak

oauth는 별도의 패키지로 사용되고 있으며 보안을 위해 client id와 client secret은 환경변수로 설정함 ( hub.extraEnv 참고 )

아래 파일 참고하면 확인할 수 있음 ( OAUTH_CLIENT_ID, OAUTH_CLIENT_SECRET )

https://github.com/jupyterhub/oauthenticator/blob/main/oauthenticator/oauth2.py

### 참고: 유저 공통 비밀번호 세팅 (dummy)

https://z2jh.jupyter.org/en/stable/administrator/authentication.html

### 참고: helm 설치 방법 (수동)

https://z2jh.jupyter.org/en/stable/jupyterhub/installation.html#initialize-a-helm-chart-configuration-file

```
helm upgrade --cleanup-on-fail --install jupyterhub jupyterhub/jupyterhub --namespace jupyter --create-namespace --version=4.0.0 -f ./values-override.yaml
```