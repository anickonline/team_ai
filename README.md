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
</p>

---

## 简介

TeamAI 是一个 AI 员工调度与协作平台，让企业可以创建、管理和调度多个 AI 员工，协同完成复杂任务。支持任务分解、多智能体协作、AI 主持会议、实时消息、工作流自动化等能力。QQ群交流：134287
<img width="1284" height="2283" alt="qrcode_1777638068197" src="https://github.com/user-attachments/assets/ec74f0f1-c379-4cb3-8c01-ad92dd5080fa" />


## 核心特性

### AI 员工管理

- 创建和配置多种类型的 AI 员工：助手、分析师、开发者、设计师、写手、研究员、经理等
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

## 功能截图

<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192456_localhost" src="https://github.com/user-attachments/assets/0e2ecbc2-37a4-49be-86e9-c10516e6b8e5" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192440_localhost" src="https://github.com/user-attachments/assets/edbde571-c118-406b-9c4d-daf817710f17" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193259_192 168 1 4" src="https://github.com/user-attachments/assets/e0efafca-f447-49a0-9726-a0c75b90c36d" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193248_192 168 1 4" src="https://github.com/user-attachments/assets/2717bb79-e388-406e-93fe-173676fc6143" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193238_192 168 1 4" src="https://github.com/user-attachments/assets/1a025556-6607-4360-b062-97adb59aa0db" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193227_192 168 1 4" src="https://github.com/user-attachments/assets/84e6ed31-18d8-425d-bf1f-626411c6f7d1" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193158_192 168 1 4" src="https://github.com/user-attachments/assets/a7e2a005-e0f4-4b8d-bff8-acda6c1262c3" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193149_192 168 1 4" src="https://github.com/user-attachments/assets/7f88d227-e119-47d2-97bf-6ea1f5bae684" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193139_192 168 1 4" src="https://github.com/user-attachments/assets/28849d6a-607d-4372-b406-414caca26c6c" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193127_192 168 1 4" src="https://github.com/user-attachments/assets/cbf14857-c9f8-4a03-9a2f-eca3b9c4c159" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193110_192 168 1 4" src="https://github.com/user-attachments/assets/837f616a-aa6c-48ac-b6e7-6ea7c6f8def6" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193034_192 168 1 4" src="https://github.com/user-attachments/assets/67db2ba1-058a-449d-8110-68b16f33d987" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_193017_192 168 1 4" src="https://github.com/user-attachments/assets/bb779c45-7e34-4f7d-9ce5-a370129580a3" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192949_localhost" src="https://github.com/user-attachments/assets/711882b1-8bda-473b-87a5-a3c6c2174ba3" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192934_localhost" src="https://github.com/user-attachments/assets/e0037449-f450-4ad4-a8d1-e2b33af43faf" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192916_localhost" src="https://github.com/user-attachments/assets/1aa0f37e-6ad4-4d23-9cbf-850d185e1bb2" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192859_localhost" src="https://github.com/user-attachments/assets/c21da2ee-0a68-482a-9cb3-87209768b224" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192846_localhost" src="https://github.com/user-attachments/assets/3e79b2f8-ada9-4464-819f-162ecf2b4fcc" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192837_localhost" src="https://github.com/user-attachments/assets/cc969ab9-fbfd-4bc1-a81f-0156a0d36829" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192825_localhost" src="https://github.com/user-attachments/assets/f8ecb035-6f0e-4136-b32a-d2ca282558bb" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192743_localhost" src="https://github.com/user-attachments/assets/9f4db7f4-dd6e-4144-93cb-b0e48ce0bee9" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192657_localhost" src="https://github.com/user-attachments/assets/80f26e75-e7b8-4b4d-8967-0b948437cd2e" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192644_localhost" src="https://github.com/user-attachments/assets/a54f992b-6d54-4532-ae9e-3e5ac86b40d6" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192628_localhost" src="https://github.com/user-attachments/assets/d936a0d6-61f9-4fc5-911d-1ee7534b439a" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192530_localhost" src="https://github.com/user-attachments/assets/34493add-7026-41c8-9b06-e17eebb18b57" />
<img width="2434" height="1247" alt="屏幕截图_1-5-2026_192517_localhost" src="https://github.com/user-attachments/assets/2c4b36d4-3684-4140-9f43-78c0727093ad" />
