## Manifest
Kubernetesは所謂Infrastructure as Codeのアプローチが可能です。  

各種Objectsをyamlで定義することができ、このコードのことを **Manifest** と呼びます。  
基本的にプロダクションでKubernetesを使用する場合はコマンドよりコードで管理すると良いでしょう。

## コードの生成
先程実行したコマンドからyamlを生成してみましょう。
```console
$ kubectl create deployment handson --image=nginx --dry-run -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: handson
  name: handson
spec:
  replicas: 1
  selector:
    matchLabels:
      app: handson
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: handson
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```


## 既存Objectsのyamlを確認
既存のObjectsもyamlで確認することが可能です。  
`--output yaml` オプションを使うことでyamlで現在のコード(yaml)を確認できます。

```console
$ kubectl get deployment/handson --output yaml
```
