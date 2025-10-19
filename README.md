# software
软工课设
# 科研成果管理系统后端

## 项目简介

本项目是科研成果管理系统的后端服务，基于Go语言和Gin框架开发，使用JWT进行身份认证，MySQL作为数据库存储。

## 技术栈

- Go语言
- Gin Web框架
- GORM ORM框架
- MySQL数据库
- JWT认证

## 项目结构

```
backend/
├── api/                # API接口实现
│   ├── achievement.go  # 成果管理相关接口
│   ├── api.go          # 基础API（登录、用户信息等）
│   ├── audit.go        # 审核相关接口
│   ├── department.go   # 部门管理接口
│   ├── excel.go        # Excel导入导出
│   ├── file.go         # 文件上传下载
│   ├── log.go          # 日志相关接口
│   ├── statistics.go   # 统计数据接口
│   └── user.go         # 用户管理接口
├── config/             # 配置文件
│   ├── config.go       # 配置加载
│   └── config.yaml     # 配置文件
├── middleware/         # 中间件
│   ├── auth.go         # JWT认证中间件
│   └── cors.go         # 跨域中间件
├── model/              # 数据模型
│   └── model.go        # 数据库模型定义
├── router/             # 路由
│   └── router.go       # 路由注册
├── uploads/            # 上传文件存储目录
└── utils/              # 工具函数
    ├── hash.go         # 密码哈希
    ├── jwt.go          # JWT工具
    ├── log.go          # 日志工具
    └── response.go     # 响应格式化
```

## 主要功能

1. **用户认证**：基于JWT的登录认证系统
2. **用户管理**：用户的CRUD操作
3. **部门管理**：部门的CRUD操作
4. **成果管理**：科研成果的提交、审核、查询等
5. **文件管理**：支持文件上传下载
6. **数据统计**：成果统计分析
7. **日志记录**：系统操作日志

## API接口

### 认证相关

- `POST /api/login`：用户登录
- `POST /api/logout`：用户登出
- `GET /api/profile`：获取个人信息
- `PUT /api/profile`：更新个人信息
- `PUT /api/profile/password`：修改密码

### 用户管理

- `GET /api/users`：获取用户列表
- `POST /api/users`：创建用户
- `PUT /api/users/:id`：更新用户
- `DELETE /api/users/:id`：删除用户
- `POST /api/users/:id/reset_password`：重置密码

### 部门管理

- `GET /api/departments`：获取部门列表
- `POST /api/departments`：创建部门
- `PUT /api/departments/:id`：更新部门
- `DELETE /api/departments/:id`：删除部门

### 成果管理

- `POST /api/achievements`：创建成果
- `GET /api/achievements/my`：获取我的成果
- `GET /api/achievements`：获取所有成果（管理员）
- `GET /api/achievements/:id`：获取成果详情
- `PUT /api/achievements/:id`：更新成果
- `POST /api/achievements/:id/submit`：提交成果
- `POST /api/achievements/:id/audit`：审核成果

## 开发环境配置

1. 安装Go环境（推荐Go 1.16+）
2. 安装MySQL数据库
3. 克隆项目代码
4. 修改`config/config.yaml`配置文件
5. 运行`go mod tidy`安装依赖
6. 运行`go run main.go`启动服务

## 配置说明

配置文件位于`config/config.yaml`，主要包含以下配置：

```yaml
app:
  port: 8080          # 服务端口
database:
  dsn: "用户名:密码@tcp(数据库地址:端口)/数据库名?charset=utf8mb4&parseTime=True&loc=Local"
  maxIdleConns: 10    # 最大空闲连接数
  maxOpenConns: 100   # 最大打开连接数
jwt:
  secret: "密钥"       # JWT密钥
  expire: 86400       # JWT过期时间（秒）
upload:
  dir: "./uploads"    # 上传文件存储目录
  maxSize: 10         # 最大上传大小（MB）
```

## 部署说明

1. 编译项目：`go build -o app main.go`
2. 运行服务：`./app`

也可以使用Docker部署：

```bash
# 构建Docker镜像
docker build -t edu-system-backend .

# 运行容器
docker run -p 8080:8080 edu-system-backend
```
# 科研成果管理系统前端


基于 Vue 3 + Element Plus 的科研成果管理系统前端项目。

## 功能特性

- 🔐 **用户认证** - 登录/登出、权限控制
- 👥 **用户管理** - 用户CRUD、批量操作、导入导出
- 🏢 **部门管理** - 部门信息管理
- 📊 **成果管理** - 成果填报、审核、统计
- 📈 **数据统计** - 多维度数据分析和可视化
- 📝 **系统日志** - 操作记录和审计

## 技术栈

- **Vue 3** - 组合式API
- **Vue Router 4** - 路由管理
- **Pinia** - 状态管理
- **Element Plus** - UI组件库
- **Axios** - HTTP客户端
- **Vite** - 构建工具
- **ECharts** - 数据可视化

## 项目结构

```
src/
├── api/                    # API接口层
│   ├── auth.js            # 认证相关
│   ├── users.js           # 用户管理
│   ├── departments.js     # 部门管理
│   ├── achievements.js    # 成果管理
│   ├── files.js          # 文件管理
│   ├── statistics.js     # 统计功能
│   └── logs.js           # 系统日志
├── components/            # 公共组件
│   ├── AppHeader.vue      # 头部导航
│   └── AppSidebar.vue    # 侧边栏
├── layouts/               # 布局组件
│   ├── MainLayout.vue    # 主布局
│   └── AuthLayout.vue    # 认证布局
├── pages/                # 页面组件
│   ├── Login.vue         # 登录页
│   ├── Dashboard.vue     # 仪表板
│   ├── Profile.vue       # 个人中心
│   ├── Users/            # 用户管理
│   ├── Departments/      # 部门管理
│   ├── Achievements/     # 成果管理
│   ├── Statistics/       # 统计页面
│   └── Logs/            # 系统日志
├── router/               # 路由配置
├── store/                # 状态管理
├── utils/                # 工具类
├── App.vue              # 根组件
└── main.js              # 入口文件
```

## 快速开始

### 1. 安装依赖

```bash
npm install
```

### 2. 启动开发服务器

```bash
npm run dev
```

### 3. 构建生产版本

```bash
npm run build
```

## 主要功能模块

### 认证系统
- 用户登录/登出
- Token自动管理
- 路由权限控制
- 角色权限区分

### 用户管理
- 用户列表（分页、搜索、筛选）
- 用户新增/编辑/删除
- 批量操作
- 密码重置
- 导入导出功能

### 成果管理
- 成果类型配置（论文、专利、项目等）
- 成果填报表单
- 成果列表和详情
- 审核流程管理
- 文件附件上传

### 统计功能
- 数据统计概览
- 按类型统计
- 按年份统计
- 按部门统计
- 图表可视化

## 权限控制

### 角色权限
- **管理员**：拥有所有功能权限
- **教职工**：只能管理自己的成果

### 路由权限
- 认证路由：需要登录
- 管理员路由：需要管理员权限
- 公开路由：登录页面

## 开发说明

### 环境要求
- Node.js >= 16
- npm >= 8

### 开发规范
- 使用组合式API
- 遵循Vue 3最佳实践
- 统一的代码风格
- 完善的错误处理

### 部署说明
1. 构建项目：`npm run build`
2. 部署到Web服务器
3. 配置反向代理到后端API

## 许可证

MIT License

