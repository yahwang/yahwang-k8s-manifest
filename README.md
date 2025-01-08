# yahwang-k8s-manifest

구조 참고 : https://cloudogu.com/en/blog/gitops-repository-patterns-part-6-examples#example-5-the-path-to-gitops

```
yahwang-k8s-manifest/
├── apps   
│   └── jupyterhub
│   └── kafka-ui
│   └── strimzi-kafka
├── bootstrap
│   └── applicationsets      # cluster-config 배포
├── cluster-config
│   └── base
│   └── overlays
│   │   └── cert-manager
│   │   └── grafana
│   │   └── harbor
│   │   └── ingress-nginx
│   │   └── jenkins
│   │   └── keycloak
│   │   └── loki
│   │   └── operators        # operator 관리
│   │   └── redis
│   └── secrets              # secret template 저장
│   └── pvcs                 # 볼륨 고정을 위한 pvc 미리 생성
│   └── README.md            # cluster-config 설정 관련 문서
└── components
│   └── applicationsets      # apps 배포
│   └── appset-template.yaml # apps 배포 템플릿
```