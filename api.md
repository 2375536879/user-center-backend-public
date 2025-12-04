# 用户中心 API 文档

## 1. 项目介绍

用户中心系统提供用户注册、登录、注销、信息查询等基础功能，支持管理员权限控制。

## 2. 接口列表

| API路径 | 方法 | 功能描述 | 权限要求 |
| :--- | :--- | :--- | :--- |
| `/user/register` | `POST` | 用户注册 | 无 |
| `/user/login` | `POST` | 用户登录 | 无 |
| `/user/logout` | `POST` | 用户注销 | 登录用户 |
| `/user/current` | `GET` | 获取当前登录用户信息 | 登录用户 |
| `/user/search` | `GET` | 根据用户名搜索用户 | 管理员 |
| `/user/delete` | `POST` | 删除用户 | 管理员 |

## 3. 接口详情

### 3.1 用户注册

**URL**: `/user/register`
**方法**: `POST`
**功能**: 注册新用户
**请求体参数**:

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| `userAccount` | `String` | 是 | 用户账号 |
| `userPassword` | `String` | 是 | 用户密码 |
| `checkPassword` | `String` | 是 | 校验密码（必须与密码一致） |
| `planetCode` | `String` | 是 | 星球编号 |

**请求示例**:
```json
{
  "userAccount": "test123",
  "userPassword": "password123",
  "checkPassword": "password123",
  "planetCode": "123456"
}
```

**响应示例**:
```json
{
  "code": 0,
  "data": 1,
  "message": "操作成功",
  "description": "注册成功"
}
```

**失败响应示例**:
```json
{
  "code": 40000,
  "data": null,
  "message": "参数错误",
  "description": "账号密码不能为空"
}
```

### 3.2 用户登录

**URL**: `/user/login`
**方法**: `POST`
**功能**: 用户登录系统
**请求体参数**:

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| `userAccount` | `String` | 是 | 用户账号 |
| `userPassword` | `String` | 是 | 用户密码 |

**请求示例**:
```json
{
  "userAccount": "test123",
  "userPassword": "password123"
}
```

**响应示例**:
```json
{
  "code": 0,
  "data": {
    "id": 1,
    "username": "测试用户",
    "userAccount": "test123",
    "avatarUrl": "https://example.com/avatar.jpg",
    "gender": 0,
    "phone": "13800138000",
    "email": "test@example.com",
    "userStatus": 0,
    "createTime": "2024-01-01T00:00:00",
    "updateTime": "2024-01-01T00:00:00",
    "userRole": 0,
    "planetCode": "123456"
  },
  "message": "操作成功",
  "description": "登录成功"
}
```

### 3.3 用户注销

**URL**: `/user/logout`
**方法**: `POST`
**功能**: 用户退出登录
**权限要求**: 已登录用户
**请求体**: 无

**响应示例**:
```json
{
  "code": 0,
  "data": 1,
  "message": "操作成功",
  "description": "注销成功"
}
```

### 3.4 获取当前用户信息

**URL**: `/user/current`
**方法**: `GET`
**功能**: 获取当前登录用户的信息
**权限要求**: 已登录用户
**请求参数**: 无

**响应示例**:
```json
{
  "code": 0,
  "data": {
    "id": 1,
    "username": "测试用户",
    "userAccount": "test123",
    "avatarUrl": "https://example.com/avatar.jpg",
    "gender": 0,
    "phone": "13800138000",
    "email": "test@example.com",
    "userStatus": 0,
    "createTime": "2024-01-01T00:00:00",
    "updateTime": "2024-01-01T00:00:00",
    "userRole": 0,
    "planetCode": "123456"
  },
  "message": "操作成功",
  "description": "获取成功"
}
```

### 3.5 搜索用户

**URL**: `/user/search`
**方法**: `GET`
**功能**: 根据用户名模糊搜索用户
**权限要求**: 管理员
**查询参数**:

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| `username` | `String` | 否 | 用户名关键词（支持模糊搜索） |

**响应示例**:
```json
{
  "code": 0,
  "data": [
    {
      "id": 1,
      "username": "测试用户",
      "userAccount": "test123",
      "avatarUrl": "https://example.com/avatar.jpg",
      "gender": 0,
      "phone": "13800138000",
      "email": "test@example.com",
      "userStatus": 0,
      "createTime": "2024-01-01T00:00:00",
      "updateTime": "2024-01-01T00:00:00",
      "userRole": 0,
      "planetCode": "123456"
    }
  ],
  "message": "操作成功",
  "description": "搜索成功"
}
```

### 3.6 删除用户

**URL**: `/user/delete`
**方法**: `POST`
**功能**: 根据用户ID删除用户
**权限要求**: 管理员
**请求体参数**:

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| `id` | `long` | 是 | 用户ID |

**请求示例**:
```json
{
  "id": 1
}
```

**响应示例**:
```json
{
  "code": 0,
  "data": true,
  "message": "操作成功",
  "description": "删除成功"
}
```

## 4. 数据结构

### 4.1 基础响应结构

```json
{
  "code": 0,               // 状态码，0表示成功，其他表示失败
  "data": {},              // 响应数据，具体类型根据接口而定
  "message": "操作成功",    // 响应消息
  "description": "成功描述"  // 详细描述
}
```

### 4.2 用户实体

| 字段名 | 类型 | 描述 |
| :--- | :--- | :--- |
| `id` | `long` | 用户ID |
| `username` | `String` | 用户昵称 |
| `userAccount` | `String` | 用户账号 |
| `avatarUrl` | `String` | 用户头像URL |
| `gender` | `Integer` | 性别 |
| `phone` | `String` | 电话号码 |
| `email` | `String` | 邮箱地址 |
| `userStatus` | `Integer` | 用户状态，0表示正常 |
| `createTime` | `Date` | 创建时间 |
| `updateTime` | `Date` | 更新时间 |
| `userRole` | `Integer` | 用户角色，0表示普通用户，1表示管理员 |
| `planetCode` | `String` | 星球编号 |

## 5. 错误码说明

| 错误码 | 描述 |
| :--- | :--- |
| `0` | 成功 |
| `40000` | 参数错误 |
| `40100` | 未登录 |
| `40300` | 无权限 |
| `50000` | 系统内部错误 |

## 6. 权限说明

- 普通用户：可以访问注册、登录、注销、获取当前用户信息接口
- 管理员：可以访问所有接口，包括搜索用户和删除用户接口

## 7. 注意事项

1. 所有需要登录的接口都通过Session进行身份验证
2. 管理员权限判断基于用户角色字段(`userRole`)
3. 密码在存储时会进行加密处理
4. 用户查询结果会自动过滤敏感信息