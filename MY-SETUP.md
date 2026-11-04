# my-custom（这是我自己用的变种，不是给上游的）

基线：**官方 0.13.6**（`3bff816`）。
在上面叠了两层：

1. **PR #45 的改动**（`feat/bili-detail-config`）——B站 详情长度配置化 + 评论字数配置化。作者还没合，先自己用。
2. **两处本地偏好**（上游没有开关的）：
   - `lib/life.js`：日程兜底文案「在家待着 / 处理正事」+ 日程有空洞时按 `idle` 处理（`gap: true`）
   - `lib/stickers.js`：`DIR_CAP` 300 → 1200（表情包目录能放更多）

## 装法

```bash
# 在新机器 / 新 profile 里
pnpm add github:xmlyyds666/dsh-fish-soul#my-custom
```

然后把 `dsh.profile.bundles` 里加上 `dsh-fish-soul`（如果还没有）。

## 跟版

官方发新版后：

```bash
git fetch upstream
git rebase upstream/main      # 会有冲突，冲突基本都在上面三个文件
```

冲突处理原则：**上游优先**，只把「两处本地偏好」重新叠回去；PR #45 若已被上游合入，就把第 1 层整个丢掉。

## 注意

- 这个分支**不发 npm、不发 Release**，只给我自己装。
- 用它的 profile 不要再同时用 `patches/dsh-fish-soul@x.y.z.patch`，否则补丁会和分支改动打架（补丁是按官方 tarball 打的，行号对不上）。
