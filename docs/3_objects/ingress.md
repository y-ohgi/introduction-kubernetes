![ingress](imgs/ingress.png)

## Ingressとは
ロードバランサとしての機能を提供するObjectです。

Ingressは（L7）ロードバランサとしての機能を持ち、受け付けたトラフィックをServiceへルーティングします。  
GKEの場合マネージドロードバランサであるGoogle Cloud Load Balancer（以降GCLB）との連携を簡単に行えるので、今回はGCLBの使用を前提とします

## 作成する
（IngressはCLIからの作成に対応していないため、）Manifestを用意します。  
`ingress.yaml` というファイルを作成しましょう。

```console
$ vi ingress.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  labels:
    app: mynginx
  name: mynginx

spec:
  replicas: 1
  selector:
    matchLabels:
      app: mynginx
  template:
    metadata:
      labels:
        app: mynginx
    spec:
      containers:
      - image: nginx:latest
        name: mynginx

---
apiVersion: v1
kind: Service

metadata:
  labels:
    app: mynginx
  name: mynginx

spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: mynginx
  type: NodePort

---
apiVersion: extensions/v1beta1
kind: Ingress

metadata:
  name: mynginx

spec:
  backend:
    serviceName: mynginx
    servicePort: 80
```
