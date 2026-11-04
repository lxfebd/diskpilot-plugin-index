# DiskPilot 官方插件索引

本仓库托管 DiskPilot 插件市场的**官方社区索引** `index.json`（schema 1，Ed25519 签名信封），以及首批官方插件的发布包（见 [Releases](https://github.com/lxfebd/diskpilot-plugin-index/releases)）。

- 客户端契约：[主仓库 docs/plugin-market-index.md](https://github.com/lxfebd/diskpilot/blob/main/docs/plugin-market-index.md)
- 作者发布指南：[docs/publish-plugin-guide.md](https://github.com/lxfebd/diskpilot/blob/main/docs/publish-plugin-guide.md)
- 在 DiskPilot 里使用：设置 → 插件市场 → 索引 URL 填
  `https://raw.githubusercontent.com/lxfebd/diskpilot-plugin-index/main/index.json` → 刷新

## 安全模型

- `index.json` 信封带 Ed25519 签名（覆盖整个 `plugins[]` 的规范 JSON），客户端强制验签，失败保留旧索引。
- 每个插件 zip 内 `tool.plugin.json` 带 `signature`/`signer`/`digest`（包内文件 Ed25519 签名），安装时强制验签且签名者必须等于索引条目声明的 `signer`。
- 索引条目必须带 zip 的 `sha256`，客户端下载后强校验。
- CI（`.github/workflows/validate-index.yml`）在每次 PR/push 校验：schema=1、必填字段、url 必须 https、有 url 必有 sha256、id 必须 kebab-case。

## 社区作者上架

把你的插件 zip 上传到任意 https 直链（推荐自己仓库的 Releases），然后提 PR 修改 `index.json` 的 `plugins[]`（模板见主仓库 publish-plugin-guide.md）。PR 通过 CI 后合并即生效。
