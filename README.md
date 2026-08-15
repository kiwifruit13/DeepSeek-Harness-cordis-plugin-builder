# cordis-plugin-builder

**从零构建 Cordis 可用插件：完整教学 + 实战指导 + 避坑手册**

DeepSeek Harness（DSH）底层是 **Cordis 元框架**（"一切皆插件"）。本技能是围绕它打造的**插件构建全链路指南**——从"元框架是什么"讲起，到建立概念地图、引导从零构建、能力挂载、部署打包，再到卸载与排障，覆盖插件开发的全生命周期。

---

## 一、技能定位

| 维度 | 说明 |
|---|---|
| **类型** | DSH 可加载技能（`SKILL.md` + 15 个 `references/` 参考文档） |
| **适用对象** | 想构建/修改/部署 DSH 插件的人；插件开发教学、答疑、排障 |
| **核心主张** | 教学式结构：先建立概念心智地图，再按 8 步流程构建，最后交付部署 |
| **触发方式** | 构建、编写、修改或部署 Cordis 插件时；插件开发指导、教学或答疑；讲解 Cordis 元框架概念；排查插件加载失败（PENDING/FAILED） |

**一句话**：不只是一本"怎么用"的手册，更是一张"怎么理解"的地图——先懂元框架，再动手写插件。

---

## 二、核心内容（SKILL.md 结构）

```
第 0 节  元框架核心概念  五要素脑图（Context/Plugin/Fiber/effect/Event）+ 10 概念速查 + 哲学
第 1 节  从零构建 8 步   定位命名 → 选形态 → 契约先行 → 声明依赖 → 注册副作用 → 装配 → 验证 → 部署
第 2 节  格式与规格      导出项 / 扁平命名空间 / Config 校验 / TS 声明合并 等硬约束
第 3 节  关键坑（实测）   9 条高频坑速查（waterfall/insert/file:// 等）
第 4 节  检查清单        14 项交付前检查（契约/副作用/能力挂载/事件/Client/内核/部署/卸载/打包）
第 5 节  详细参考        15 个 references 按学习路径排序
```

---

## 三、目录结构

```
cordis-plugin-builder/
├── SKILL.md                  # 主入口：概念 → 构建 → 规格 → 坑 → 清单 → 参考
└── references/               # 15 个参考文档（渐进披露，按需深挖）
    ├── 概念层
    │   ├── dsh-platform.md          # DSH 平台全景（预设模式/构建路径/生态/环境）
    │   ├── philosophy.md            # 核心理念 / Context 作用域 / DSH 魔改
    │   ├── mental-models.md         # 认知模型（加载机制/形态正交/选型口诀）
    │   └── api-contract.md          # CLAUDE.md 公约 → 插件语境映射
    ├── 结构层
    │   ├── plugin-forms.md          # 三种代码形态 / Service / Config / inject 模板
    │   ├── lifecycle.md             # Fiber 状态机 / effect / HMR
    │   ├── events.md                # 五种事件分发模式 / waterfall 语义
    │   └── events-catalog.md        # DSH 事件目录（选择脑图 + 高频事件）
    ├── 能力层
    │   ├── harness-integration.md   # 模型工具 / 提示词 / 技能 / Client UI / 权限
    │   ├── client-ui.md             # Slot 选择脑图 / 注册协议 / 主题 / host.call
    │   └── dynamic-plugins.md       # 动态插件生命周期 / Builtin / 版本授权 / 修复
    └── 交付层
        ├── deployment-overview.md  # 六种部署形态 / 七种流程 / 卸载 / 选择矩阵
        ├── packaging.md            # 打包 / cordis.yml / npm pack / 诊断 PENDING
        ├── testing.md              # 测试方法论（真实 Context 单测范式）
        └── traps.md                # 31 个实测坑（坑分类总览）
```

> 每个 reference 都带 **ASCII 局部脑图**（决策树/状态机/流程图），零依赖、终端可读。

---

## 四、安装与部署

### 方式 A：DSH 技能目录（watcher 即时生效）

```powershell
# 解压 zip → 把 cordis-plugin-builder/ 放入技能根目录
Expand-Archive cordis-plugin-builder.zip -DestinationPath C:\Users\kiwif\.agents\skills
# 目录名必须与 frontmatter name 一致（kebab-case），watcher 即时加载，无需重启
```

### 方式 B：手工放置

```powershell
Copy-Item cordis-plugin-builder C:\Users\kiwif\.agents\skills\ -Recurse
```

### 合规验证

```bash
node E:\Deepseek\check-skills.mjs cordis-plugin-builder
# 期望：✅ 通过（name kebab-case / frontmatter 完整 / SKILL.md ≤500 行）
```

---

## 五、快速上手

1. **先读大局**：`references/dsh-platform.md` —— DSH 是什么、四种预设模式、插件怎么进系统。
2. **建立概念**：SKILL.md 第 0 节 —— 元框架五要素（Context/Plugin/Fiber/effect/Event）一张图。
3. **从零构建**：SKILL.md 第 1 节 —— 8 步流程，逐步实现你的第一个插件。
4. **产出能力**：`references/harness-integration.md` —— 让插件真正被模型调用（工具/提示词/技能/UI）。
5. **交付部署**：`references/deployment-overview.md` + `packaging.md` —— 选形态、装配、打包、卸载。

**遇到问题先查**：SKILL.md 第 3 节关键坑（9 条）→ `references/traps.md`（31 条实测）→ 运行时 `cordis_inspect_*` 实时查契约。

---

## 六、设计原则

| 原则 | 说明 |
|---|---|
| **教学式结构** | 概念（怎么理解）→ 结构（怎么写）→ 能力（产出什么）→ 交付（怎么上线）→ 坑库（别踩什么） |
| **渐进披露** | SKILL.md 是地图（一句话 + 入口），细节全在 references——按需深挖，不一次灌满 |
| **实测优先** | 事件目录/Slot 树/服务契约均来自运行时 `cordis_inspect_*` 实测，非推测 |
| **脑图即地图** | 每个 reference 带 ASCII 局部脑图，先看结构再读细节 |
| **API 演进友好** | 运行时 API 以 `cordis_inspect_*` 实时查询为准，技能文档是"地图"而非"死数据" |

---

## 七、版本记录

| 版本 | 日期 | 内容 |
|---|---|---|
| 0.1 | 2026-08 | 初始构建（三种形态/流程/坑库） |
| 0.2 | 2026-08 | 进阶：六种部署形态 / 七种流程 / 卸载 / npm pack / 认知模型 / 能力挂载 / Client UI / 动态插件 / 事件目录 / 多语言内核 |
| 0.3 | 2026-08 | 重构为教学式结构；补 DSH 平台全景；13 个 references 全加局部脑图；文档引用全量核验（33 链接零缺失）；zip 打包分发 |

---

## 八、维护约定

- **SKILL.md ≤ 500 行**：超限内容拆进 `references/`（一级深，勿嵌套）。
- **frontmatter**：`name` 必须 kebab-case 且与目录名一致；`description` 写触发判别句式。
- **交付前**：跑 `node E:\Deepseek\check-skills.mjs <name>` 合规检测。
- **引用纪律**：references 内部互引用 `[name](name.md)` 相对链接；外部引用（DSH checkout 文档）注明位置。
