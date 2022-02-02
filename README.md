# DokC K8ssandra-lightweight helm-chart
Custom K8ssandra operator for Date on Kuberenetes' how-to-dok project.
This chart contains the kubernetes operator for cassandra as a stack, it includes:
  1.  Apache Cassandra
  2.  Prometheus and Grafana
  3.  Stargate
 
 
 There are provisions to enable packages like Medusa and Reaper, You can enable them by adding them to the [dependencies](https://github.com/AbhijithGanesh/dokc-helm-chart/blob/510ad7c0ffe14a056b05cc67339f5205811cfd91/Chart.yaml#L2-L21) and enable the [values](https://github.com/AbhijithGanesh/dokc-helm-chart/blob/510ad7c0ffe14a056b05cc67339f5205811cfd91/values.yaml#L180) to enable these containers
 
 
 <h1> Installation and requirements </h1>
 
 <h3> Requirements </h3> 
 
  - CPU Cores = 4
  - RAM = 8128m
<h3> Installation </h3>
 To Install this package:
 
 You can add it through:
 
 `helm repo add dokc https://abhijithganesh.github.io/dokc-helm-chart/`
 
 This will add your package into local helm repository list.
 To verify this , run the command
 `helm repo list`
 
 It must show `dokc` as list.
 
 Once the repository is listed, you can run your k8ssandra cluster, but this would require a YAML file which would like this
 ```yml
 cassandra:
  version: <Cassandra Version Number, preferred version = 4.0.1> 
  cassandraLibDirVolume:
    storageClass: local-path
    size: 5Gi
  allowMultipleNodesPerWorker: true
  heap:
   size: 1G
   newGenSize: 1G
  resources:
    requests:
      cpu: 1000m
      memory: 2Gi
    limits:
      cpu: 1000m
      memory: 2Gi
  datacenters:
  - name: <Data Center Name>
    size: <Size>
    racks:
    - name: < Rack Name >
    
kube-prometheus-stack:
  grafana:
    adminUser: < Grafana Admin User >
    adminPassword: <Grafana Password>
    
    
stargate:
  enabled: <Boolean>
  replicas: 1
  heapMB: 256
  cpuReqMillicores: 200
  cpuLimMillicores: 1000
  
```
 
 To run the cluster, execute the following command:
 `helm install -f <filename>.yaml <Instance Name (or) Cluster Name> dokc/dokc-chart`
 
 
 <h2> Credits </h2>
 Thanks to K8ssandra.io who's the maker of [ k8ssandra.io ](https://github.com/k8ssandra/k8ssandra/) chart, the chart was pivotal and it was an inspiration to this chart.
