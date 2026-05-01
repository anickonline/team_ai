<p align="center">
  <img src="frontend/src/assets/vue.svg" alt="TeamAI Logo" width="80" height="80" />
  <h1 align="center">TeamAI</h1>
  <p align="center">AI 员工调度与协作平台</p>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Vue-3.x-42b883" />
  <img src="https://img.shields.io/badge/NestJS-11.x-e0234e" />
  <img src="https://img.shields.io/badge/TypeORM-0.3-ff6f61" />
  <img src="https://img.shields.io/badge/PostgreSQL-15+-336791" />
  <img src="https://img.shields.io/badge/Redis-5+-dc382d" />
  <img src="https://img.shields.io/badge/License-MIT-blue" />
</p>

---

## 简介

TeamAI 是一个 AI 员工调度与协作平台，让企业可以创建、管理和调度多个 AI 员工，协同完成复杂任务。支持任务分解、多智能体协作、AI 主持会议、实时消息、工作流自动化等能力。

## 截图

<table>
  <tr>
    <td align="center">仪表盘</td>
    <td align="center">任务管理</td>
  </tr>
  <tr>
    <td><img src="" alt="dashboard" /></td>
    <td><img src="" alt="tasks" /></td>
  </tr>
  <tr>
    <td align="center">协作看板</td>
    <td align="center">AI 会议</td>
  </tr>
  <tr>
    <td><img src="" alt="board" /></td>
    <td><img src="" alt="meeting" /></td>
  </tr>
  <tr>
    <td align="center">消息中心</td>
    <td align="center">员工管理</td>
  </tr>
  <tr>
    <td><img src="" alt="message" /></td>
    <td><img src="" alt="employee" /></td>
  </tr>
</table>

## 核心特性

### AI 员工管理

- 创建和配置 7 种类型的 AI 员工：助手、分析师、开发者、设计师、写手、研究员、经理
- 自定义系统提示词、模型选择、能力配置（文本生成、代码生成、图像分析、数据分析、网页搜索、文件处理、翻译）
- 四层记忆系统：灵魂层、身份层、长期记忆、工作记忆，支持自动提炼
- 员工状态实时监控（在线、离线、忙碌、异常）

### 任务管理与调度

- 完整的任务生命周期：待处理 → 进行中 → 已完成/已取消/失败
- 三种视图：列表视图、日历视图、甘特图
- 任务优先级（低、中、高、紧急）和批量操作
- AI 驱动的任务分解为子任务
- 任务依赖关系图（完成-开始、开始-开始、完成-完成、开始-完成）
- 执行监控：迭代追踪、工具调用日志、Token 用量

### 多智能体协作

- 并行执行：多个 AI 员工同时处理不同子任务
- 顺序执行：按依赖关系依次处理
- 执行+审查：AI 完成后由另一个 AI 审查，最多 3 轮返工
- 协作看板：拖拽式看板，WebSocket 实时同步，冲突解决

### AI 会议室

- AI 主持人驱动的会议，支持多种发言模式：自由讨论、轮流发言、主持人控制、举手发言
- 会议议程管理、密码保护、参与者角色（主持人、发言人、参会者）
- 实时语音/输入状态指示
- AI 自动生成会议纪要（摘要、要点、决议、行动项、投票结果）
- 行动项可直接转化为任务

### 实时消息

- 私聊和群聊
- 联系人列表（用户 + AI 员工）
- @提及（包括 @AI 员工、@所有人）
- 消息类型：文本、图片、文件
- 消息回复、引用、撤回、删除
- 输入状态、已读/未读、免打扰

### 自动化与集成

- **定时任务**：间隔、每日、每周、每月、一次性、Cron 表达式，支持重叠策略
- **工作流**：事件触发的自动化规则（条件 + 动作）
- **Webhook**：出站 HTTP 回调，HMAC 签名验证，投递日志
- **MCP 服务**：Model Context Protocol 集成，本地和远程服务，扩展 AI 工具能力
- **技能系统**：可安装的技能包（知识、工具、工作流、混合类型）

### 系统管理

- 组织机构管理：层级式组织树，员工分配
- 用户与角色管理：RBAC 权限体系，细粒度权限控制
- 权限设置：危险工具确认、风险命令拦截、自动审批开关
- 健康监控：CPU、内存、磁盘、网络、服务延迟趋势
- 审计日志：完整操作审计（用户、资源、操作、IP）
- Token 用量分析：按员工、按模型的消耗统计，日/小时级图表
- 数据维护：手动/自动备份，数据库导入恢复
- 回收站：全模块软删除与恢复
- 全局搜索：跨任务、员工、消息搜索

## 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | Vue 3 + TypeScript + Vite + Element Plus + ECharts |
| 后端 | NestJS + TypeScript + TypeORM + Passport + JWT |
| 数据库 | PostgreSQL 15+ |
| 缓存 | Redis 5+ |
| 实时通信 | WebSocket (Socket.IO) |
| 部署 | Docker Compose / PM2 / 原生 |

## 快速开始

### 环境要求

- Node.js 18.x 或 20.x LTS
- PostgreSQL 15+
- Redis 5+

### 开发模式

```bash
# 克隆项目
git clone https://github.com/your-username/TeamAI.git
cd TeamAI

# 安装依赖
cd backend && npm install
cd ../frontend && npm install

# 配置环境变量
cd backend
cp .env.example .env
# 编辑 .env 填入数据库和 Redis 连接信息

# 启动后端
npm run start:dev

# 启动前端（新终端）
cd frontend
npm run dev
```

### 生产部署

```bash
# 打包
./publish.sh

# 部署（在目标机器上）
cd scripts
./start.ps1      # Windows
./start.sh       # Linux
```

详见 [DEPLOY.md](DEPLOY.md)。

## 项目结构

```
TeamAI/
├── backend/                  # 后端 (NestJS)
│   ├── src/
│   │   ├── modules/          # 业务模块 (30个)
│   │   ├── common/           # 公共模块 (guards, decorators, filters...)
│   │   └── main.ts           # 入口
│   ├── package.json
│   └── tsconfig.json
├── frontend/                 # 前端 (Vue 3)
│   ├── src/
│   │   ├── views/            # 页面 (22个)
│   │   ├── components/       # 组件
│   │   ├── api/              # API 接口
│   │   ├── store/            # Pinia 状态
│   │   ├── router/           # 路由
│   │   ├── i18n/             # 国际化 (中/英)
│   │   └── utils/            # 工具函数
│   └── package.json
├── nginx/                    # Nginx 配置
├── scripts/                  # 启动脚本
├── publish.sh                # 打包脚本
├── CHANGELOG.md              # 更新说明
└── docker-compose.yml        # Docker 编排
```

## 多语言

支持中文和英文界面切换。

## 许可证

Copyright © 2026 成都致易科技有限公司. All rights reserved.

本软件为非开源软件。社区版可免费使用，但源代码受版权保护，
不得修改、再分发或商业转售。详见 LICENSE 文件。
