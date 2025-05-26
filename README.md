# おうちKubernetes構築手順（Ansible + kubeadm + Vault）

このREADMEは、お家でKubenetesを作成する構成を管理しています。

---

## ネットワーク構成

* Podネットワーク: `10.244.0.0/16`
* Serviceネットワーク: `10.96.0.0/12`
* ノードネットワーク: `192.168.8.128/25`
- master ノードネットワーク: `192.168.8.128/27`
- worker ノードネットワーク: `192.168.8.160/27`

## 対象ノード

* master01（192.168.8.129）: Ansible実行ノード + control-plane
* worker01（192.168.8.161）
* worker02（192.168.8.162）

## 設定方法

### Orange Pi B3 にOSをインストール

### Orange Pi B3 のSSDにOSをインストール

### 初期設定(Security)

### Ansibleの設定

### NFSの設定

### Kubenetesの導入

#### Orange Pi B3 スペック

| 項目         | 内容                                                  |
| ---------- | --------------------------------------------------- |
| **CPU**    | Rockchip RK3566（4コア ARM Cortex-A55、最大1.8GHz）        |
| **GPU**    | Mali-G52 2EE                                        |
| **RAM**    | 2GB / 4GB / 8GB LPDDR4（モデルにより異なる）                   |
| **ストレージ**  | microSDスロット + eMMCスロット（オプション） + SPI Flash（容量小）      |
| **USB**    | USB 3.0 x1、USB 2.0 x2、USB Type-C（電源＆データ）            |
| **HDMI**   | HDMI 2.0（4K出力対応）                                    |
| **ネットワーク** | Gigabit Ethernet、有線LAN（RJ45）ポートあり                   |
| **Wi-Fi**  | 802.11ac Wi-Fi + Bluetooth 5.0（オンボード）               |
| **GPIO**   | 26ピン（Raspberry Pi互換に近い）                             |
| **OSサポート** | Ubuntu / Debian / Android / Orange Pi OS（Debian系）など |
