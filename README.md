# おうちKubernetes構築手順（Ansible + kubeadm + Vault）

このREADMEは、お家でKubenetesを作成する構成を管理しています。

---

## ネットワーク構成

* Podネットワーク: `10.244.0.0/16`
* Serviceネットワーク: `10.96.0.0/12`
* ノードネットワーク: `192.168.8.128/25`

## 対象ノード

* master01（192.168.8.129）: Ansible実行ノード + control-plane
* worker01（192.168.8.161）
* worker02（192.168.8.162）

