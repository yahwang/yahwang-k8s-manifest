https://github.com/apache/airflow/tree/helm-chart/1.16.0

### production 배포 가이드

https://airflow.apache.org/docs/helm-chart/stable/production-guide.html

### ArgoCD로 배포 시 주의사항

values-overrides.yaml아래 부분이 2군데 존재하는데 

비활성화를 해야 DB MIGRATION이 동작하게 되어 있음

```
useHelmHooks: false # ArgoCD로 배포하는 경우 비활성화
applyCustomEnv: false # ArgoCD로 배포하는 경우 비활성화
```

### airflow-webserver-config template

아래는 ConfigMap으로 sealed secret이 적용이 안 되는 부분이라 수동으로 생성 ( client_secret 주의 )

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: airflow-webserver-config
  namespace: common
data:
  webserver_config.py: |-
    import os
    import jwt
    import requests
    import logging
    from base64 import b64decode
    from cryptography.hazmat.primitives import serialization
    from flask_appbuilder.security.manager import AUTH_OAUTH
    from airflow import configuration as conf
    from airflow.www.security import AirflowSecurityManager

    log = logging.getLogger(__name__)

    AUTH_TYPE = AUTH_OAUTH
    AUTH_USER_REGISTRATION = True
    AUTH_ROLES_SYNC_AT_LOGIN = True
    AUTH_USER_REGISTRATION_ROLE = "Admin" # 유저 최초 로그인 시 역할 지정
    PERMANENT_SESSION_LIFETIME = 3600
    OIDC_ISSUER = "https://keycloak.yahwang.cloud/realms/dev-tools"

    OAUTH_PROVIDERS = [
        {
            "name": "keycloak",
            "icon": "fa-key",
            "token_key": "access_token",
            "remote_app": {
                "client_id": "airflow",
                "client_secret": ".........................",
                "server_metadata_url": "https://keycloak.yahwang.cloud/realms/dev-tools/.well-known/openid-configuration",
                "api_base_url": "https://keycloak.yahwang.cloud/realms/dev-tools/protocol/openid-connect",
                "client_kwargs": {"scope": "openid email profile"},
                "access_token_url": "https://keycloak.yahwang.cloud/realms/dev-tools/protocol/openid-connect/token",
                "authorize_url": "https://keycloak.yahwang.cloud/realms/dev-tools/protocol/openid-connect/auth",
                "request_token_url": None,
            },
        }
    ]
```

참고자료:

- https://airflow.apache.org/docs/apache-airflow-providers-fab/stable/auth-manager/webserver-authentication.html#example-using-team-based-authorization-with-keycloak

- https://honglab.tistory.com/339

- https://flask-appbuilder.readthedocs.io/en/latest/security.html
