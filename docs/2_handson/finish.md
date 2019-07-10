ここまで作成してきたObjectsを削除しましょう。

## 何を作ったのか
まずは今まで作ってきたObjectsを確認してみましょう。
```console
$ kubectl get all
NAME                            READY   STATUS    RESTARTS   AGE
pod/handson-5676646c85-vwkxd    1/1     Running   0          78m
pod/handson2-6d99688857-x746j   1/1     Running   0          4m56s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/handson      LoadBalancer   10.3.243.4   34.85.67.170   80:32621/TCP   4m
service/kubernetes   ClusterIP      10.3.240.1   <none>         443/TCP        2h

NAME                       DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/handson    1         1         1            1           124m
deployment.apps/handson2   1         1         1            1           4m56s

NAME                                  DESIRED   CURRENT   READY   AGE
replicaset.apps/handson-5676646c85    1         1         1       124m
replicaset.apps/handson2-6d99688857   1         1         1       4m56s
```

後ほど詳細を説明しますが、作成したのは大きく3つです。

1. "handson"
    - Deployment, ReplicaSet, Pod
2. handson用の"ロードバランサ"
    - Service
3. "handson2"
    - Deployment, ReplicaSet, Pod

## 削除
順番に削除していきましょう

### handson
コンテナの削除
```console
$ kubectl delete deploy/handson
deployment.extensions "handson" deleted
```

ロードバランサの削除
```console
$ kubectl delete service/handson
```

コンテナの削除
```console
$ kubectl delete -f manifest.yaml
```
