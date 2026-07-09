# silicon-market

Silicon Worker 的**能力市场仓**——一个纯静态的 git 仓库，托管可分享的**技能 / 专家 / 团队**。零托管成本：push 到 GitHub / Gitee 等，应用通过 raw URL 按需拉取。

本仓初始内容由 Silicon Worker 内置精选（builtin-catalog）一次性生成：**16 个专家 + 9 个团队**（多数携带技能）。

## 在应用里使用

Silicon Worker →「设置 → 市场来源 → 添加市场来源」，粘贴本仓的 **raw 基址**，例如托管在 GitHub 时：

```
https://raw.githubusercontent.com/<owner>/silicon-market/main/
```

应用会拉 `market.json` 发现有哪些货架，浏览时按需拉分片与详情，点「加入我的」即可安装到本地。

## 目录格式

```
market.json                          # 瘦根：{name, version, updatedAt, shelves}
market_expert.json                   # 专家列表分片（发现元数据）
market_team.json                     # 团队列表分片
experts/<name>/
  ├── expert.md                      # frontmatter(name/description/category/scenario/tags/featured/order/…) + 正文
  └── skills/<skill>/SKILL.md        # 该专家携带的技能
teams/<name>/
  ├── team.json                      # {displayName, quickPrompts, members:[{name, role, displayName}], …}
  ├── experts/<member>.md            # lead(role:lead) + 各成员(role:member)
  └── skills/<skill>/SKILL.md        # 团队携带的技能
```

- 条目标识 = `name` == 目录段（必须是 `[a-z0-9-]` slug、单类货架内唯一）。
- 列表页元数据放分片；正文 / roster 放各条目详情文件，按需拉取。
- 缺某类货架就从 `market.json.shelves` 里省略对应键。

## 维护

- 新增 / 修改条目后，重新生成索引：编辑 `experts/`、`teams/` 下的文件，然后重建 `market.json` + 分片（保持格式一致）。
- 建议用 PR + CI 校验 `market.json` / frontmatter 格式（零成本）。
- `skill` 货架：在顶层新增 `skills/<name>/SKILL.md` 并补 `market_skill.json` 分片即可。

## 来源

由 [silicon-worker](https://github.com/) 的 T101「远程能力市场」生成。内容版权归各自作者。
