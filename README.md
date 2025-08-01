# yahwang-k8s-manifest

구조 참고 : https://cloudogu.com/en/blog/gitops-repository-patterns-part-6-examples#example-5-the-path-to-gitops

```
yahwang-k8s-manifest/
├── apps   
│   └── airflow
│   └── datahub
│   └── jupyterhub
│   └── kafka-ui
│   └── schema-registry
│   └── strimzi-kafka
│   └── elasticsearch-eck
├── bootstrap
│   └── applicationsets      # cluster-config 배포
│   │   └── sealed-secrets-manager # sealed-secrets 전체 배포 manager
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
│   │   └── nessie
│   │   └── operators        # operator 관리
│   │   └── prometheus
│   │   └── redis
│   └── sealed-secrets       # sealed-secrets + reflector를 통한 시크릿 관리
│   └── pvcs                 # 볼륨 고정을 위한 pvc 미리 생성
│   └── README.md            # cluster-config 설정 관련 문서
└── components
│   └── applicationsets      # apps 배포
│   └── appset-template.yaml # apps 배포 템플릿
```

## [Dashboard 구성](https://github.com/yahwang/yahwang-k8s-manifest/blob/main/Dashboard.md)

## Cluster 구성

- Longhorn을 통해 PVC 활용 ( storageclass )

- MetalLB를 통해 LoadBalancer에 IP 할당

- Nginx Ingress Controller를 활용해 ingress 배포

- Cert Manager와 Let's encrypt를 활용해 ingress에 https 적용

- prometheus와 grafana를 활용한 모니터링

- keycloak oidc 일부 적용

![Cluster 구성](https://drive.usercontent.google.com/download?id=1OV9Pfna_z3KyK1pZ4VpERXu6DV26YRbF)

## 참고

- 싱글 노드의 maxPods 개수 변경

k9s로 node describe를 보면 기본 값이 노드당 110개 POD 제한을 알 수 있음

```
Capacity:
    ...
    pods: 110
```

```
# sudo vim /var/lib/kubelet/config.yaml

maxPods: 200 # 추가
```

수정 후 kubelet 재시작

```
sudo systemctl restart kubelet
```

