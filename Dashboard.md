# 대시보드 구성

## Kubernetes Dashboard

![Cluster 대시보드](https://drive.google.com/uc?export=view&id=1AXqYjWtzojpKkER3wuJ_NAXRwwupgaiv)

- 기본 대시보드 : https://grafana.com/grafana/dashboards/18283-kubernetes-dashboard/

  - kube-prometheus-stack에서 metric 수집 pod 설치
  
  - kubelet service 생성해서 cadvisor 메트릭 수집

  - container 메트릭의 경우, container!=""를 추가해서 중복 계산을 방지 (POD의 정보를 제외한다는 의미)

    - 예시 : container_cpu_usage_seconds_total{namespace=~"$namespace", container!="")

- 참고

  - kube-state-metrics: https://github.com/kubernetes/kube-state-metrics

  - node-exporter: https://github.com/prometheus/node_exporter

## POD 로그 수집

![로그 대시보드](https://drive.google.com/uc?export=view&id=1XhUcgUVnzSekmhbqZdVk5x-zDNx2Fda1)

- Vector Agent를 통해 로그를 수집

  - Loki로 데이터를 sink하여 저장

  - namespace마다 agent와 pipeline 배포 ( vector operator 배포 특징 )

- 참고

  - [vector-log-agent 배포](https://github.com/yahwang/yahwang-k8s-manifest/tree/main/apps/vector-log-agent/overlays/dev)


## 기타

  - Kubernetes Kafka Topics : https://grafana.com/grafana/dashboards/10122-kafka-topics/

  - Strimzi KRaft 클러스터 모니터링 : https://github.com/strimzi/strimzi-kafka-operator/blob/main/examples/metrics/grafana-dashboards/strimzi-kraft.json