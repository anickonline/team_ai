# TeamAI 部署指南

## 环境要求

| 组件 | 版本 |
|------|------|
| Node.js | 18.x 或 20.x LTS |
| PostgreSQL | 15.x |
| Redis | 5.x+ |

## 前置准备

### PostgreSQL

在 psql 中创建用户（需具有 CREATEDB 权限）：

```sql
-- 使用 postgres 超级用户登录 psql 后执行：
CREATE USER teamai WITH PASSWORD 'teamai123' CREATEDB;
```

> 如果你想使用已有的 postgres 超级用户，也可以，后续启动时输入对应的用户名和密码即可。

### Redis

安装后默认即可，无需额外配置。如果 Redis 设置了密码，启动时需要输入。

## 快速开始

### 方式 A: 使用启动脚本（推荐）

**Windows PowerShell:**

```powershell
cd scripts
.\start.ps1
```

**Linux / macOS:**

```bash
cd scripts
bash start.sh
```

首次运行会进入交互式配置：

```
============================================
  First-time setup
============================================

  [PostgreSQL]
  Database host [localhost]:          ← 回车默认 localhost
  Database port [5432]:               ← 回车默认 5432
  PostgreSQL username [teamai]:       ← 回车默认 teamai
  PostgreSQL password [teamai123]:    ← 回车默认 teamai123
  Database name [teamai]:             ← 回车默认 teamai

  [Redis]
  Redis host [localhost]:             ← 回车默认 localhost
  Redis port [6379]:                  ← 回车默认 6379
  Redis password (leave empty if none):  ← 有密码则输入，无则回车
```

脚本会自动：
1. 创建 `.env` 配置文件
2. 安装依赖（如 node_modules 不存在）
3. 检测 PostgreSQL 连接，若数据库不存在则自动创建
4. 启动后端和前端服务
5. 自动创建管理员账号（admin / admin123）

### 方式 B: 手动启动

```bash
cd backend
cp .env.example .env
# 编辑 .env 填入数据库和 Redis 连接信息
npm ci --production
npm run start:prod
```

首次启动时后端会自动：
- 生成 `JWT_SECRET` 和 `ENCRYPTION_MASTER_KEY`（如果仍是默认值）
- 检测并创建 PostgreSQL 数据库（如果不存在）
- 安装 PostgreSQL 扩展（uuid-ossp, pgcrypto）
- 通过 TypeORM synchronize 自动创建所有数据表
- 启动成功后将 `.env` 中 `DB_INITIALIZED` 设为 `true`，`NODE_ENV` 设为 `production`
- 后续启动将跳过数据库初始化

### 方式 C: PM2 生产部署

```bash
npm install -g pm2
pm2 start ecosystem.config.js --env production
pm2 save
```

### 方式 D: Docker Compose

```bash
docker compose up -d --build
```

## 验证

| 服务 | 地址 |
|------|------|
| 前端 | http://localhost:5173 |
| 后端 API | http://localhost:3000/api (Swagger 文档) |
| 版本信息 | http://localhost:3000/api/system-settings/version |
| 默认账号 | admin / admin123 |

## 目录结构

```
├── backend/           # 后端 (NestJS)
│   ├── dist/          # 编译产物
│   ├── package.json   # 依赖声明（含版本号）
│   └── .env.example   # 环境变量模板
├── frontend/
│   └── dist/          # 前端构建产物 (静态文件)
├── nginx/
│   └── nginx.conf     # Nginx 配置
├── scripts/
│   ├── start.ps1      # Windows 启动脚本
│   └── start.sh       # Linux 启动脚本
├── ecosystem.config.js # PM2 配置
└── docker-compose.yml  # Docker 编排
```
