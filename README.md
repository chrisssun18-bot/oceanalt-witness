# OceanAlt · Public Audit Witness / 公开审计见证

This repository is OceanAlt's **public, tamper-evident witness** of its audit ledger.
本仓库是 [OceanAlt](https://media.oceanalt.com) 审计账本的**公开、防篡改见证**。

## What's here / 这里有什么

Only **fingerprints** — nothing else. No source code, no articles, no database, no user data, no secrets.
只有**指纹**,别无他物:没有源码、文章、数据库、用户数据或任何密钥。

- [`witness/latest.json`](witness/latest.json) — the most recent fingerprint of the audit-ledger tip, plus its Bitcoin anchor proof.
- [`witness/history.log`](witness/history.log) — one line per recorded fingerprint (UTC time · SHA-256 · run id). Git history makes this append-only and tamper-evident.

Each fingerprint is a **one-way SHA-256 hash** of OceanAlt's hash-chained audit log. You cannot reverse it to recover any content; changing a single byte upstream changes the hash entirely.
每条指纹是 OceanAlt 哈希链审计日志的**单向 SHA-256 摘要**——无法反推出任何原文;上游改动一个字节,哈希就完全不同。

## How to verify independently / 如何独立验证

1. Take any `fingerprint` from `witness/latest.json` (or any past entry in `history.log`).
2. The `bitcoinAnchor.otsProofBase64` is an [OpenTimestamps](https://opentimestamps.org) proof. Verify it at **https://opentimestamps.org** — this checks the fingerprint against the Bitcoin blockchain and **does not depend on OceanAlt in any way**.
3. Because the record lives in this public repo's Git history *and* is anchored to Bitcoin, rewriting OceanAlt's audit history would require rewriting this repo, the Bitcoin chain, and OceanAlt's own ledger simultaneously — which is why it is tamper-evident.

拿任意一条指纹,用其 `otsProofBase64` 到 opentimestamps.org 对着比特币链验证即可——**整个过程不依赖 OceanAlt**。

## Cadence / 更新频率

A scheduled GitHub Action in this repo pulls the public endpoint
`https://media.oceanalt.com/api/audit-anchor` every few hours and commits the fingerprint here. The endpoint is public; this repo needs no credentials from OceanAlt.

## Links

- Proof & audit page: https://media.oceanalt.com/en/proof
- Standard (RAP): https://media.oceanalt.com/en/rap
