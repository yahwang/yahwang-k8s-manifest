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