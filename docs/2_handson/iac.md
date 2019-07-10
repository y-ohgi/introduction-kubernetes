## Manifest
Kubernetesは所謂Infrastructure as Codeのアプローチが可能です。  

各種Objectsをyamlで定義することができ、このコードのことを **Manifest** と呼びます。  
基本的にプロダクションでKubernetesを使用する場合はコマンドよりコードで管理すると良いでしょう。

## コードの生成
先程実行したコマンドからyamlを生成可能です。  
まずは"handson2"という名前でコンテナを立ち上げるyamlを表示してみます。 `--dry-run` `-o yaml` がポイントです。
```console
$ kubectl create deployment handson2 --image=nginx --dry-run -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: handson2
  name: handson2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: handson2
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: handson2
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```

先程表示したyamlをファイルへ書き込みましょう。
```console
$  kubectl create deployment handson2 --image=nginx --dry-run -o yaml > manifest.yaml
```

`kubectl apply` でコードを実行する事が可能です。
```console
$ kubectl apply -f manifest.yaml
```

"handson2" が作成されたか確認してみましょう。
```console
$ kubectl get deployment/handson2
NAME       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
handson2   1         1         1            1           13s
```

## 既存Objectsのyamlを確認
既存のObjectsもコードで確認することが可能です。  
`--output yaml` オプションを使うことでyamlで現在のコード(yaml)を確認できます。

```console
$ kubectl get deployment/handson2 --output yaml
```
