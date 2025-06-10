# API 接口文档

本文档详细介绍了 FIVC Journey 旅游全程追踪系统的所有API接口。

## 👨‍💻 作者

**Charlie ZHANG**  
📧 Email: sunnypig2002@gmail.com

## 🌐 基础信息

- **Base URL**: `http://localhost:8000`
- **API 版本**: `v1`
- **API 前缀**: `/api/v1`
- **认证方式**: JWT Bearer Token
- **数据格式**: JSON

## 📖 在线文档

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

> 💡 **提示**: 推荐使用在线文档进行API测试，本文档主要用于参考。

## 🔐 认证流程

### 获取访问令牌

大多数API端点需要认证。首先需要注册用户并获取访问令牌：

1. **注册用户**: `POST /api/v1/auth/register`
2. **用户登录**: `POST /api/v1/auth/login`
3. **使用令牌**: 在请求头中添加 `Authorization: Bearer <token>`

## 📋 API 端点总览

### 🔐 认证相关 (`/api/v1/auth`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/register` | 用户注册 | ❌ |
| POST | `/login` | 用户登录 | ❌ |

### 👤 用户管理 (`/api/v1/users`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| GET | `/me` | 获取当前用户信息 | ✅ |
| PUT | `/me` | 更新当前用户信息 | ✅ |
| GET | `/{user_id}` | 获取用户信息 | ✅ |

### 🗺️ 旅行计划 (`/api/v1/travel-plans`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/` | 创建旅行计划 | ✅ |
| GET | `/` | 获取旅行计划列表 | ✅ |
| GET | `/{plan_id}` | 获取旅行计划详情 | ✅ |
| PUT | `/{plan_id}` | 更新旅行计划 | ✅ |
| DELETE | `/{plan_id}` | 删除旅行计划 | ✅ |

### 📅 行程安排 (`/api/v1/itineraries`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/` | 创建行程安排 | ✅ |
| GET | `/travel-plan/{plan_id}` | 获取旅行计划的行程列表 | ✅ |
| GET | `/{itinerary_id}` | 获取行程详情 | ✅ |
| PUT | `/{itinerary_id}` | 更新行程安排 | ✅ |
| DELETE | `/{itinerary_id}` | 删除行程安排 | ✅ |

### 💰 费用记录 (`/api/v1/expenses`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/` | 创建费用记录 | ✅ |
| GET | `/` | 获取费用记录列表 | ✅ |
| GET | `/statistics` | 获取费用统计 | ✅ |
| GET | `/{expense_id}` | 获取费用记录详情 | ✅ |
| PUT | `/{expense_id}` | 更新费用记录 | ✅ |
| DELETE | `/{expense_id}` | 删除费用记录 | ✅ |

### 📝 旅行日志 (`/api/v1/travel-logs`)

| 方法 | 端点 | 描述 | 认证 |
|------|------|------|------|
| POST | `/` | 创建旅行日志 | ✅ |
| GET | `/` | 获取旅行日志列表 | ✅ |
| GET | `/my` | 获取我的旅行日志 | ✅ |
| GET | `/public/latest` | 获取最新公开日志 | ❌ |
| GET | `/{log_id}` | 获取旅行日志详情 | ✅ |
| PUT | `/{log_id}` | 更新旅行日志 | ✅ |
| DELETE | `/{log_id}` | 删除旅行日志 | ✅ |

## 🔍 详细API说明

### 认证相关

#### 用户注册

```http
POST /api/v1/auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com", 
  "password": "securepassword123",
  "full_name": "John Doe",
  "phone": "+1234567890"
}
```

#### 用户登录

```http
POST /api/v1/auth/login
Content-Type: application/x-www-form-urlencoded

username=john_doe&password=securepassword123
```

### 旅行计划

#### 创建旅行计划

```http
POST /api/v1/travel-plans/
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Tokyo Adventure",
  "description": "Amazing trip to Tokyo",
  "destination": "Tokyo, Japan",
  "start_date": "2024-06-01",
  "end_date": "2024-06-07",
  "budget": 2000.00,
  "currency": "USD",
  "tags": ["adventure", "culture", "food"]
}
```

## 📊 响应格式

### 成功响应

```json
{
  "data": {...},
  "message": "操作成功",
  "timestamp": "2024-01-01T12:00:00Z"
}
```

### 错误响应

```json
{
  "detail": "错误描述",
  "error_code": "ERROR_CODE",
  "timestamp": "2024-01-01T12:00:00Z"
}
```

## 🔧 状态码

| 状态码 | 描述 |
|-------|------|
| 200 | 成功 |
| 201 | 创建成功 |
| 400 | 请求错误 |
| 401 | 未认证 |
| 403 | 权限不足 |
| 404 | 资源不存在 |
| 422 | 数据验证错误 |
| 500 | 服务器错误 |

## 🔗 相关链接

- [在线API文档 (Swagger)](http://localhost:8000/docs)
- [数据模型文档](./models.md)
- [快速开始指南](./quick-start.md) 