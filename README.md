# yahwang-k8s-manifest

구조 참고 : https://cloudogu.com/en/blog/gitops-repository-patterns-part-6-examples#example-5-the-path-to-gitops

```
yahwang-k8s-manifest/
├── apps   
│   └── custom-apps
├── bootstrap
│   └── applicationsets # cluster-config 배포
├── cluster-config
│   └── base
│   └── overlays
│   │   └── operators   # operator 관리
│   │   └── ingress-nginx
│   │   └── harbor
│   │   └── keycloak
│   └── secrets         # secret template 저장
└── components
│   └── applicationsets # apps 배포
```