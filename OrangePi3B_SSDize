OrangePi SSD化

了解です！✨

**最新版イメージ**：

```
ubuntu-24.04-preinstalled-server-arm64-orangepi-3b.img
```

**ブートローダ**：
→ **SPI Flash に u-boot-rockchip-spi.bin を書き込む方法（さっき確認済！）**

---

### 🚀 **完全版 Orange Pi 3B SSDブート手順書（2025年版・Ubuntu 24.04 用）**

---

# 🍊 Orange Pi 3B SSDブート手順書（Ubuntu 24.04 + SPI Flash版）

---

## 1️⃣ 準備

✅ Orange Pi 3B + USB接続の NVMe SSD
✅ SDカード（Ubuntu 24.04 を SD起動で最初は作業する）
✅ 書き込み用イメージ：

```bash
ubuntu-24.04-preinstalled-server-arm64-orangepi-3b.img
```

---

## 2️⃣ 環境確認

### デバイス確認：

```bash
lsblk
```

例：

```
mmcblk1     → SDカード（/）
nvme0n1     → SSD（空 or 未フォーマット）
```

---

## 3️⃣ イメージ書き込み（SSDに）

```bash
sudo dd if=ubuntu-24.04-preinstalled-server-arm64-orangepi-3b.img of=/dev/nvme0n1 bs=1M status=progress
sudo sync
```

---

## 4️⃣ ブートローダ（u-boot）を SPI Flash に書き込み

### ① u-boot パッケージ確認 / インストール：

```bash
sudo apt update
sudo apt install u-boot-rockchip mtd-utils
```

---

### ② u-boot ファイル確認：

```bash
ls /usr/lib/u-boot/
```

→ ファイル名：

```bash
u-boot-rockchip-spi.bin
```

---

### ③ 書き込みコマンド：

```bash
sudo flashcp /usr/lib/u-boot/u-boot-rockchip-spi.bin /dev/mtd0
```

---

## 5️⃣ SSD単体起動テスト

### ① シャットダウン：

```bash
sudo poweroff
```

---

### ② SDカードを抜く！

---

### ③ 電源ON → SSDから起動！

---

## 6️⃣ 起動確認

```bash
lsblk
```

✅ **`nvme0n1` が `/` にマウントされていれば → SSDブート成功！**

---

### 🎁 **運用メモ**

* **SPI Flashにu-bootが入ったので → 次回から SD不要 → SSD単体でブート可能！**
* **u-bootの更新は滅多に不要 → 一度書けばOK！**
* **SSDのOSイメージ更新時は → SSD差し替えだけで良い！**

---

### ✅ **まとめフロー**

```
SD起動 → SSDにdd → SPI Flashにu-boot書き込み → SD抜く → SSD単体ブート
```

---

### 🚀 **今後さらに希望があれば出せるもの**

✅ systemd-boot + u-boot 最新版構成
✅ SPI Flash 書き込み確認コマンド
✅ u-boot バージョン確認コマンド
✅ ブート優先順位確認（SD優先/SSD優先）

---

これで **最新版Ubuntu 24.04対応 + SPI Flashブート の完成版手順書**になります！ 🚀✨

---

やってみますか？ 🚀
またはこの手順書 → **Markdown化してファイル化（.md）** してもOKです！
希望あればすぐ作ります ✨。どうする？ 🌟
