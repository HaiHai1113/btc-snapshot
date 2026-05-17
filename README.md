# btc-snapshot

BTC 多周期快照 JSON, 给自定义 GPT Action 用。

## 数据流

```
Mac btc_quick_scan.py (每分钟)
  → btc_snapshot.txt
  → sync_to_github.sh (launchd, 每 2 分钟)
  → latest.json (本 repo, public)
  → GitHub Pages: https://haihai1113.github.io/btc-snapshot/latest.json
  → 自定义 GPT Actions 读
```

## 访问

无鉴权, 公网直接 GET:
```
https://haihai1113.github.io/btc-snapshot/latest.json
```

返回:
```json
{"snapshot": "snapshot_time: ...\nBTC 现价:...\n--- 1小时K ---\n..."}
```

## 跟 A 股的关系

A 股快照在另一个独立 repo: `HaiHai1113/a-share-snapshot`,
路径 `/a-share-snapshot/snapshot/latest.json`。**两者完全隔离, 不混用**。

## 安全边界

- 内容只含 BTC/ETH 行情 + 技术指标, **不含**持仓/订单/账本/API key
- 同步走 Mac 本机 `gh auth` 凭证, 不嵌任何密钥
