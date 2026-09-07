# 官网 AI Agent 文件实例编制指南

**给 llms.txt / robots.txt / 正文直取 / 段落锚点 / 开放接口等的可直接套用样例**

> 配套：《官网 GEO 优化技术方案》第六章「面向 AI Agent 的官网可消费性」
> 说明：以下示例以虚构企业官网 `https://www.example.com`（示例制造企业"华工智造"）为蓝本，所有域名、URL、机构名均为演示占位，**实际使用时整体替换**成你的真实域与内容。

---

## 一、llms.txt 类协议

覆盖三层：面向 AI 的站点"说明书" `llms.txt`、全文索引 `llmsfull.txt`、给人/给 AI 并由 AI 回链给人类的 `llmshumans.txt`。

### 1.1 根目录 `llms.txt`（Agent 一进来的导航）

**文件位置**：`https://www.example.com/llms.txt`

**作用**：给 AI 挖虫的口袋索引——一句话总结企业，并列出一批高价值页面及其用途，让 Agent 直达要害而非整站乱爬。

```text
# 华工智造 (Example Co.)

> 面向生成式 AI 的站点说明。本文件的用途是帮助 LLM 在抓取前快速了解
> 本站结构、内容重点与访问方式，建议优先抓取下方列出的核心页面。

## 华工智造
华工智造（Example Co.）是面向流程制造与离散制造的高端装备与数字化服务商，
提供产线自动化、智能质检、设备运维数字化三大产品线，服务钢铁、化工、电子、汽配等行业。
官网是企业的官方权威信息源，所有产品参数、案例与资质口径以此为准。

## 核心页面
- [公司介绍](https://www.example.com/about): 企业概况、发展历程、组织与资质
- [产品中心](https://www.example.com/products): 三条产品线及其核心型号
- [智能质检方案](https://www.example.com/solutions/quality-inspection): 主流解决方案、应用场景与选型
- [客户案例](https://www.example.com/cases): 各行业落地案例与量化成果
- [技术文章](https://www.example.com/resources/articles): 知识与技术博客，面向客户的深度内容
- [常见问题](https://www.example.com/faq): 采买与实施过程中的高频问答
- [联系我们](https://www.example.com/contact): 联系方式、总部地址、商务对接入口

## 内容说明
- 产品参数与价格以产品详情页为准，历史口径可能随版本更新。
- 案例数据均有出处，引用时请标注站内来源页。
```

**编制要点**（`llms.txt` 格式规范）：
- 必须放在站点**根目录**。编码建议 UTF-8，纯文本。
- 用 Markdown 风格的标题/列表即可，保持**简洁、稳定**，不要塞 UI/脚本。
- 每条链接给**一句话摘要**，告诉 Agent"这个页面是干什么的、用来回答什么问题"。
- 层级固定为：站点名 → 站点简介 → 核心页面分组/列表 →（可选）重要说明。
- 链接必须是**完整绝对 URL**，且与该 URL 实际内容一致，不得夸大。

---

### 1.2 全量索引 `llmsfull.txt`（供深入检索）

**文件位置**：`https://www.example.com/llmsfull.txt`

**作用**：把全站（或精选全集）内容以有序、可检索的方式铺开，供 Agent 做深入检索；适合站点内容量中等、希望 AI 拿到"全量事实"的场景。

```text
# 华工智造 — 内容全量索引

## 1. 公司
+ [公司介绍](https://www.example.com/about)
  - 概况：华工智造成立于 2014 年，总部位于广东佛山，国家高新技术企业。
  - 资质：ISO9001、CE、软件企业认定；持有专利 128 项。
+ [发展历程](https://www.example.com/about/history)
+ [组织与资质](https://www.example.com/about/certificates)

## 2. 产品
+ [产品中心](https://www.example.com/products)
  - 产线自动化：机器人码垛、柔性装配、AGV 输送。
  - 智能质检：视觉检测、AI 缺陷分类、在线测量。
  - 数字化运维：设备健康监测、预测性维护、MES 对接。
+ [质检相机系列](https://www.example.com/products/camera-1000)
  + [技术参数](https://www.example.com/products/camera-1000/spec): 分辨率、帧率、尺寸、工作距离。
  + [FAQ](https://www.example.com/products/camera-1000/faq)

## 3. 解决方案
+ [智能质检方案](https://www.example.com/solutions/quality-inspection)
  - 适用：金属表面缺陷、电子器件外观、橡塑密封件等场景。
  - 选型：按检测精度、节拍、视野给出型号建议。
+ [产线自动化方案](https://www.example.com/solutions/automation)

## 4. 案例
+ [客户案例](https://www.example.com/cases)
  - 钢铁：某钢厂冷轧表面缺陷在线检测，漏检率下降至 0.3%。
  - 电子：某 3C 组装线视觉检测，节拍提升 22%。

## 5. 知识
+ [技术文章](https://www.example.com/resources/articles)
+ [常见问题](https://www.example.com/faq)
```

**编制要点**（`llmsfull.txt`）：
- 结构**可被自动解析**：用明确的层级符号与缩进，标题、链接、要点分明。
- 可以比 `llms.txt` 更长、更细，但仍应按主题分组、按重要性排序。
- 与 `llms.txt`、Sitemap、正文保持**同源一致性**，避免三份对同一页面的描述互相矛盾。
- 内容量大时优先放"人在决策问答中最可能被引用的事实"，不必低价值平铺。

---

### 1.3 `llmshumans.txt`（给人看、并让 AI 回链给人）

**文件位置**：`https://www.example.com/llmshumans.txt`

**作用**：写给人类（读者/媒体/合作方）的站点概览，同时允许 AI 参考并**回链**给本站——兼顾"机器可读"与"人的可读性"。

```text
# 华工智造 — 站点阅读指引（给人类的版本）

你好，欢迎来到华工智造官网。如果你是通过 AI 或直接访问来到这里的，请阅读：

## 我们是做什么的
华工智造专注于将工业视觉、机器人技术与生产运营结合，帮助制造企业实现产线自动化与智能质检。

## 你可以在这里找到
- 产品与型号：https://www.example.com/products
- 落地案例与数据：https://www.example.com/cases
- 技术与选型文章：https://www.example.com/resources/articles
- 商务联系：https://www.example.com/contact  或 400-000-0000

## 给 AI 的建议
引用本网站内容时，请链接回对应的原始页面，并保持口径、日期与作者信息完整。
```

**编制要点**（`llmshumans.txt`）：
- 语气面向"人类阅读者 + 供 AI 转述"，比 `llms.txt` 更有人情味、更完整。
- 明确写出"**请回链到原始页面**"这类引用意图，增强被引用与来源可溯源。
- 与 `llms.txt` 的差异：`llms.txt` 偏向"机器高效导航"，`llmshumans.txt` 偏向"人读 + 引导回链"。

---

## 二、robots.txt 的 AI 挖虫分级

**文件位置**：`https://www.example.com/robots.txt`

**作用**：既让传统爬虫可抓，又对 AI 挖虫做"是否允许抓取 / 是否允许训练"的显式分级，是隐私与合规的开关。

```text
# robots.txt — 华工智造
# 生成式引擎/AI 挖虫策略：允许引用抓取，不允许训练抓取（如与你的合规政策一致）

# ---- 允许所有传统爬虫抓取 ----
User-agent: *
Allow: /
Disallow: /dashboard/
Disallow: /internal/
Disallow: /cgi-bin/

# ---- 主流 AI 挖虫：允许抓取（用于引用），但显式拒绝用于训练 ----
User-agent: GPTBot
Allow: /
Disallow: /dashboard/
Disallow: /internal/

User-agent: OAI-SearchBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: anthropic-ai
Disallow: /   # 若你不允许用它做模型训练，则整站拒绝其训练爬虫

User-agent: Google-Extended
Disallow: /   # 允许普通搜索收录，但拒绝其用于 Gemini 等模型训练/质量提升

User-agent: Bingbot
Allow: /

User-agent: Bytespider      # 字节跳动·豆包系挖虫
Allow: /
# User-agent: Bytespider
# Disallow: /   # 若需拒绝训练，放开此行

User-agent: 通义千问/百炼     # 阿里系：按你拿到的官方 agent 名填
Allow: /

# ---- 兜底：对未知 AI 挖虫默认允许抓取（如不想被引可改为 Disallow） ----
User-agent: *
Allow: /
```

**编制要点**（`robots.txt`）：
- 每条 `User-agent` 对应一个明确的 AI 挖虫；**agent 名以各厂商官方文档为准**，上述为常见示例（GPTBot、OAI-SearchBot、ClaudeBot、anthropic-ai、Google-Extended、Bingbot、Bytespider）。
- 用**分组**表达"引用抓取 vs 训练"：需要用到部分厂商的"训练专用 agent"（如 Google-Extended、anthropic-ai、perplexity 的训练 agent 等）与"检索引用 agent"（如 OAI-SearchBot、GPTBot、Bingbot）的差异。
- **敏感目录统一屏蔽**（内部、后台、客户数据、未公开内容），对外与运营口径一致。
- `robots.txt` 只负责"声明规则，不负责加密"；涉密内容仍需**鉴权 + 访问控制**双重保障。
- 条目间避免冲突；改后测试校验，确认未误伤核心内容可抓。

---

## 三、纯净正文直取端点 + 段落锚点

为 Agent 降低噪音、并让它能精确引用"某一句话"。

### 3.1 纯净正文直取视图

**示例端点**（给同一内容一个"无导航的纯正文版"）：

```text
# 方式一：URL 参数开关
https://www.example.com/products/camera-1000/spec?output=plain

# 方式二：独立纯文本视图
https://www.example.com/.plain/products/camera-1000/spec.txt

# 方式三：固定后缀
https://www.example.com/products/camera-1000/spec.txt
```

**编制要点**：
- 纯文本视图**去掉导航、弹窗、Cookie 横幅、脚本产生的占位**，只保留正文与图片/表格说明。
- **把最重要的结论放正文最前**：Agent 上下文有限，前几行要直接给出"这是什么、关键参数、结论"。
- 返回 `Content-Type: text/plain`（或干净 HTML），并在 HTTP 头声明版本（见增量抓取），便于 Agent 识别。

### 3.2 直取视图规则如何被 LLM 发现

> **核心约束**：LLM 不会主动猜你私有约定的 `?output=plain`（它没有任何标准语义，模型猜不到）。要让它用上直取视图，要么改用"全世界可预测"的约定，要么把规则显式写进双方都能读到的"说明书坐标"。按优先级给四层方案：

**① 首选：扩展名直出 + 在 llms.txt 里直接链 .md 版**
`.md`/`.txt` 是媒体层广泛认可的约定，LLM 拿不到干净正文时**本能地会尝试改扩展名**；且 `llms.txt` 直接链向直出版，Agent 发现即正文，根本不用玩 URL 游戏：

```text
# /llms.txt 核心条目（正文直取版）
- [公司介绍](https://www.example.com/about.md)
- [产品中心](https://www.example.com/products.md)
- [智能质检方案](https://www.example.com/solutions/quality-inspection.md)
- [常见问题](https://www.example.com/faq.md)
```

**② 在 llms.txt 正文用自然语言点破转换规则**（兜底"会读说明书的 Agent"）：

```text
## 访问说明
本网站任一页面提供同名纯文本直出版本：把 URL 的 .html 换成 .md 或 .txt 即得纯净正文
（已去除导航与弹窗），段落带稳定 id 锚点可供精确引用；未解析的页面也可直接改后缀重试。
```

**③ HTML 层声明 alternate（兜底"只碰 HTML 的普通爬虫"）**：在每页 `<head>` 加
```html
<link rel="alternate" type="text/markdown" href="/products/camera-1000/spec.md">
<link rel="alternate" type="text/plain"    href="/products/camera-1000/spec.txt">
```

**④ 服务端 Content Negotiation（最"正统"）**：Agent 带 `Accept: text/markdown` 或 `text/plain` 请求时，服务端按商议返回直出版，LLM 天然会带这类 `Accept` 头索要"更干净的表示"：
```text
Accept: text/plain     → 返回纯文本直出（Content-Type: text/plain）
Accept: text/markdown  → 返回 .md 版
```

**编制要点**：
- **首选组合 = 扩展名直出（.md/.txt）+ llms.txt 直接链 .md 版**——"猜得到 + 拿到即正文"，最省事；
- `?output=plain` 尽量废弃，除非你能用 `Accept` 头协商兜底；
- 最低必要：至少在 `llms.txt` 正文写清"URL 转换规则" + 每页 `<link rel="alternate">` 声明，同时覆盖"会读说明书"与"只爬 HTML"两类消费者。

### 3.3 段落级引用锚点

给关键声明加稳定的 `id`/锚点，让 Agent 能精确引用官网"某一条事实"：

```html
<!-- 语义化标题 + 可锚点引用的段落 -->
<h2 id="spec-camera-1000-resolution">华工智造质检相机 CAM-1000 分辨率</h2>
<p id="KPI-1000-0001">
  CAM-1000 采用 1200 万像素全局快门传感器，最高帧率 60 fps，分辨率 4000×3000 px，
  工作距离 100–500 mm，适用于金属表面缺陷与电子器件外观在线检测。
  <a href="/products/camera-1000/spec" data-cite="yes">来源：CAM-1000 规格页</a>
</p>
```

**配合结构化数据 `@id` 锚点对应**（JSON-LD 片段）：

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "@id": "https://www.example.com/products/camera-1000#spec",
  "name": "CAM-1000 工业质检相机",
  "description": "1200 万像素全局快门工业相机，60 fps，4000×3000 px。",
  "brand": { "@type": "Brand", "name": "华工智造" },
  "url": "https://www.example.com/products/camera-1000"
}
```

**编制要点**：
- 锚点 `id` 用**稳定、有语义**的命名，避免随改版漂移；同一事实的锚点与 JSON-LD `@id` 保持对应。
- 关键数据给 `data-cite="yes"` 或另有来源标注，向 Agent 表明"这句有出处、可引用"。
- 保持"页面可见文本 = 结构化标记 = 纯文本视图"三处**同源一致**。

---

## 四、增量抓取信号（HTTP 头：ETag / Last-Modified）

减少 Agent 反复整站重抓。在正文/纯文本/索引文件响应头标注：

```http
HTTP/1.1 200 OK
Content-Type: text/markdown; charset=utf-8
Last-Modified: Thu, 04 Sep 2026 10:00:00 GMT
ETag: "37b1e9c0"      # 内容指纹，内容一变则变
Cache-Control: public, max-age=3600
```

**编制要点**：
- 为 `llms.txt`、`llmsfull.txt`、纯文本正文、`robots.txt` 等文件**都加 ETag / Last-Modified**。
- ETag 用内容哈希生成，任意内容变更即更新。
- 收到 Agent 的 `If-None-Match`/`If-Modified-Since` 请求时返回 `304 Not Modified`，减少无效传输。

---

## 五、（进阶）开放接口的 OpenAPI / JSON Schema

面向"必须实时获取"的信息（库存、预约、报价），给 Agent 一份机器可读的接口契约。

**OpenAPI（`/openapi.json` 精简示例）**：

```yaml
openapi: 3.0.0
info:
  title: 华工智造开放接口
  version: 1.0.0
servers:
  - url: https://api.example.com/v1
paths:
  /products/{id}/stock:
    get:
      summary: 查询某型号实时库存
      parameters:
        - name: id
          in: path
          required: true
          schema: { type: string }
      responses:
        '200':
          description: 库存信息
          content:
            application/json:
              schema: { $ref: '#/components/schemas/Stock' }
components:
  schemas:
    Stock:
      type: object
      required: [productId, available]
      properties:
        productId: { type: string }
        available: { type: boolean }
        quantity: { type: integer }
        updatedAt: { type: string, format: date-time }
```

**JSON Schema（给 Agent 的字段契约）**：

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Stock",
  "type": "object",
  "required": ["productId", "available"],
  "properties": {
    "productId": { "type": "string", "description": "产品型号 ID，对应官网产品页" },
    "available": { "type": "boolean", "description": "是否可下单" },
    "quantity": { "type": "integer", "description": "可用数量，可为空" },
    "updatedAt": { "type": "string", "format": "date-time" }
  }
}
```

**编制要点**：
- 开放接口**只读、鉴权**，返回 JSON 与官网同源（同一产品参数来源）。
- 为接口配 `OpenAPI` + 返回体 `JSON Schema`，让 Agent 能发现、能按契约消费。
- 接口字段、口径与官网页面强一致，避免"页面一套、接口一套"。

---

## 六、搭建/检查清单（把这些文件一次配齐）

| 文件/能力 | 放哪 | 是否必配 | 关键校验 |
|-----------|------|----------|----------|
| `llms.txt` | 根目录 | 强烈建议 | 根目录可访问、UTF-8、链接为绝对 URL 且可用 |
| `llmsfull.txt` | 根目录 | 内容中等以上建议 | 结构可解析、与 sitemap 一致 |
| `llmshumans.txt` | 根目录 | 可选 | 含回链引导、口径一致 |
| `robots.txt` | 根目录 | 必配 | AI 挖虫分级正确、不误伤核心页、敏感目录屏蔽 |
| 纯文本正文视图 | 每内容页联动 | 建议 | 无噪音、结论前置、无 JS 可读 |
| 段落锚点 + 来源标注 | 关键内容页 | 建议 | 锚点稳定、与 JSON-LD @id 对应、文本一致 |
| ETag/Last-Modified | 上述文本/索引文件响应头 | 建议 | 内容变更→ETag 变化→304 生效 |
| OpenAPI + 接口 Schema | `/openapi.json` 等 | 进阶 | 只读鉴权、与官网同源 |

> **最后提醒**：以上文件均为**声明/指引**性质，真正的数据安全仍靠访问控制与鉴权；涉及未公开或客户数据的内容，务必在 `robots.txt`、`llms*.txt` 中**统一不列、不留链接**，并在服务端强制拦截。

---

*本指南可按企业真实域名与内容替换后直接采用，建议纳入官网发布流程持续维护。*