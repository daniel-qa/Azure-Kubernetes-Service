https://cwhu.medium.com/kubernetes-helm-chart-tutorial-fbdad62a8b61


# Helm 介紹與建立 Chart
```
簡單來說，Helm 就是一個管理設定檔的工具。
他會把 Kubernetes 一個服務中各種元件裡的 yaml 檔統一打包成一個叫做 chart 的集合，
然後透過給參數的方式，去同時管理與設定這些 yaml 檔案。

```

## 建立自己的  chart

```
helm create helm-demo

```
### wordpress 範例
可以看檔案目錄結構，及 yml 內容
```
https://github.com/helm/charts/tree/master/stable/wordpress


接下來我們來看看 ./helm-demo 的資料夾

.
├── Chart.yaml
├── charts
├── templates
│   ├── deployment.yaml
│   ├── ingress.yaml
│   └── service.yaml
└── values.yaml

```
