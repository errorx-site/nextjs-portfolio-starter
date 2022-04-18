---
title: 使用 kubectl 查看 pod 的 label
date: 2022/4/19
description: 为了能够使用标签选择器过滤指定的标签，我通常会给资源打上标签，但是
tag: kubectl,pod
author: EX
---

# 使用 kubectl 查看 pod 的 label

为了能够使用标签选择器过滤指定的标签，我通常会给资源打上标签，但是使用 *kubectl get pod* 不会返回任何标签的信息，就算使用 *kubectl get pod -o wide* 也仅仅是多返回了一些 *IP*、*Node* 相关的新，并不能看到 *pod* 的 *label* 信息。

*kubectl get pod*
```
$ kubectl get pod
NAME                            READY   STATUS    RESTARTS   AGE
keep-running-6bd6b9b984-n7w65   1/1     Running   0          22h
```
*kubectl get pod -o wide*
```
$ kubectl get pod -o wide      
NAME                            READY   STATUS    RESTARTS   AGE   IP           NODE             NOMINATED NODE   READINESS GATES
keep-running-6bd6b9b984-n7w65   1/1     Running   0          22h   10.1.0.151   docker-desktop   <none>           <none>
```

通过 *--help* 命令可以找到，如下信息：
```
$ kubectl get pod --help
...
--show-labels=false: When printing, show all labels as the last column (default hide labels column)
...
```

因此，使用 *kubectl get pod --show-labels* 就可以查看到 *pod* 中 *label* 的信息
```
kubectl get pod --show-labels
NAME                            READY   STATUS    RESTARTS   AGE   LABELS
keep-running-6bd6b9b984-n7w65   1/1     Running   0          22h   app=keep-running,pod-template-hash=6bd6b9b984
```