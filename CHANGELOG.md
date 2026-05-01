# 更新说明

## [1.0.1] - 2026-05-01

### 新增
- 首次部署交互式配置引导（PostgreSQL + Redis 连接信息输入）
- 首次启动自动创建数据库、安装扩展、生成 JWT_SECRET 和 ENCRYPTION_MASTER_KEY
- 首次初始化完成后自动将 NODE_ENV 切换为 production
- 系统版本号接口 `GET /api/system-settings/version`（免认证）
- 登录页和侧边栏底部显示版本号
- 打包目录名包含版本号，如 `TeamAI_v1.0.1_20260501_145518`
- publish.sh 支持交互式选择版本号升级

### 修复
- 修复 publish.sh 中 node -p 读取 package.json 输出整个对象的问题
- 修复 start.ps1 中 PostgreSQL 预检脚本 argv 索引错误
- 修复编译后 require package.json 路径不正确的问题
- 修复侧边栏版本号在菜单展开后被覆盖的布局问题
