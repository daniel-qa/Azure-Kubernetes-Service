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
#### 檔案定義

```
* Chart.yaml

定義了這個 Chart 的 Metadata，包括 Chart 的版本、名稱、敘述等

* charts

在這個資料夾裡可以放其他的 Chart，這裡稱作 SubCharts

* templates

定義這個 Chart 服務需要的 Kubernetes 元件。但我們並不會把各元件的參數寫死在裡面，而是會用參數的方式代入

* values.yaml

定義這個 Chart 的所有參數，這些參數都會被代入在 templates 中的元件。
例如我們會在這邊定義 nodePorts 給 service.yaml 、
定義 replicaCount 給 deployment.yaml、
定義 hosts 給 ingress.yaml 等等

從上面的檔案結構可以看到，
我們透過編輯 values.yaml，
就可以對所有的 yaml 設定檔做到版本控制與管理。
並透過 install / delete 的方式一鍵部署 / 刪除。


```
