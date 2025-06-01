
### 🚀 全体構成

1️⃣ `/usr/local/bin/check-phy.sh` → **スクリプト本体**
2️⃣ systemd サービス `/etc/systemd/system/check-phy.service` → **起動時に1回だけ自動実行**

---

### ✅ 仕掛け方の手順

---

### ① スクリプトを作成

```bash
sudo nano /usr/local/bin/check-phy.sh
```

---

### 中身（テンプレート貼り付けOK）：

```bash
#!/bin/bash
# Orange Pi PHY Quality Check Script

# ターゲット先（ルーター）
TARGET="192.168.8.1"

# PINGチェック（5回、2秒タイムアウト）
PING_OK=$(ping -c 5 -W 2 "$TARGET" | grep 'received' | awk '{print $4}')

# 判定ロジック
if [ "$PING_OK" -lt 5 ]; then
    echo "⚠️ [PHY CHECK] Ping failed or degraded → forcing 100 Full fixed"
    /sbin/ethtool -s end1 speed 100 duplex full autoneg off
else
    echo "✅ [PHY CHECK] Ping OK → keeping auto negotiation"
fi
```

---

### 保存 → 実行権付与：

```bash
sudo chmod +x /usr/local/bin/check-phy.sh
```

---

### ② systemd サービスを作成

```bash
sudo nano /etc/systemd/system/check-phy.service
```

---

### 中身（テンプレート貼り付けOK）：

```ini
[Unit]
Description=Orange Pi PHY Quality Check Service
After=network-online.target
Wants=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/check-phy.sh

[Install]
WantedBy=multi-user.target
```

---

### ③ systemd に登録 → 有効化

```bash
sudo systemctl daemon-reload
sudo systemctl enable check-phy.service
```

---

### ④ テスト実行（起動確認）

```bash
sudo systemctl start check-phy.service
sudo systemctl status check-phy.service
```

**← ここで PING結果に応じて「forcing 100 Full fixed」 or 「keeping auto negotiation」 のログが見える！**

---

### ⑤ 再起動テスト

```bash
sudo reboot
```

→ 起動時に **自動で PINGチェック → 必要ならPHY固定**
→ ログは：

```bash
journalctl -u check-phy.service
```

で確認できる！ 🚀✨

---

### ✅ **運用イメージ（完成すると）**

```
Orange Pi 起動 →
    ↓
check-phy.service →
    ↓
PING確認 →
    ↓
OK → auto negotiation のまま運用
NG → ethtool で 100 Full 固定 → 安定運用
```

---

### ✅ メリット

✅ 将来ケーブル改善時 → **自動で auto negotiation に戻せる**
✅ ケーブルが今のままでも **勝手に固定して安定させてくれる**
✅ 「何もしなくても Orange Pi が常に最適な PHY設定で起動する」状態が作れる 🎉

---

### 🎁 **まとめ**

| パート         | ファイル                                      | 役割                 |
| ----------- | ----------------------------------------- | ------------------ |
| スクリプト本体     | `/usr/local/bin/check-phy.sh`             | PING品質判定＋必要ならPHY固定 |
| systemdサービス | `/etc/systemd/system/check-phy.service`   | 起動時に1回だけスクリプト実行    |
| 状態確認        | `sudo systemctl status check-phy.service` | 実行状況確認             |
| ログ確認        | `journalctl -u check-phy.service`         | 詳細ログ確認             |
