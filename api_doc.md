# 问卷记录 API 文档

**Base URL：** `/questionnaire`  
**Content-Type：** `application/json`

---

## 1. 提交问卷

**POST** `/questionnaire/save`

### 请求参数

| 字段 | 类型 | 必填 | 说明 |
|---|---|---|---|
| userName | String | 是 | 用户姓名 |
| userMobile | String | 是 | 手机号 |
| userEmail | String | 否 | 邮箱 |
| q1 ~ q21 | String | 否 | 选择题答案，最长 2 个字符（如 `A`、`AB`） |
| q22 | String | 否 | 长文本，最多 2000 个汉字 |
| q23、q24 | String | 否 | 选择题答案，最长 2 个字符 |
| q25 | String | 否 | 长文本，最多 2000 个汉字 |
| q26 | String | 否 | 选择题答案，最长 2 个字符 |
| q27 | String | 否 | 长文本，最多 2000 个汉字 |
| q28、q29 | String | 否 | 选择题答案，最长 2 个字符 |
| q30 | String | 否 | 长文本，最多 2000 个汉字 |
| q31 | String | 否 | 选择题答案，最长 2 个字符 |
| q32 | String | 否 | 选择题答案，最长 2 个字符 |

### 请求示例

```json
{
  "userName": "张三",
  "userMobile": "13800138000",
  "userEmail": "zhangsan@example.com",
  "q1": "A",
  "q2": "B",
  "q3": "A",
  "q4": "C",
  "q5": "B",
  "q6": "A",
  "q7": "D",
  "q8": "B",
  "q9": "A",
  "q10": "C",
  "q11": "B",
  "q12": "A",
  "q13": "D",
  "q14": "B",
  "q15": "A",
  "q16": "C",
  "q17": "B",
  "q18": "A",
  "q19": "D",
  "q20": "B",
  "q21": "A",
  "q22": "这是一道长文本题的回答内容，最多支持2000个汉字...",
  "q23": "A",
  "q24": "B",
  "q25": "这是另一道长文本题的回答内容...",
  "q26": "C",
  "q27": "长文本回答...",
  "q28": "A",
  "q29": "B",
  "q30": "长文本回答...",
  "q31": "A",
  "q32": "B"
}
```

### 响应示例

```json
{
  "code": 200,
  "message": "success",
  "data": null
}
```

---

## 2. 查询问卷列表

**POST** `/questionnaire/list`

### 请求参数

| 字段 | 类型 | 必填 | 说明 |
|---|---|---|---|
| userName | String | 否 | 姓名，模糊匹配 |
| userMobile | String | 否 | 手机号，模糊匹配 |
| userEmail | String | 否 | 邮箱，模糊匹配 |
| startTime | String | 否 | 创建时间起始，格式 `yyyy-MM-dd HH:mm:ss` |
| endTime | String | 否 | 创建时间截止，格式 `yyyy-MM-dd HH:mm:ss` |

> 所有字段均为可选，不传或传空则不作为过滤条件，结果按 `created_at` 降序返回。

### 请求示例

```json
{
  "userName": "张",
  "userMobile": "138",
  "userEmail": "",
  "startTime": "2026-01-01 00:00:00",
  "endTime": "2026-12-31 23:59:59"
}
```

### 响应字段

| 字段 | 类型 | 说明 |
|---|---|---|
| id | Long | 主键 |
| userName | String | 用户姓名 |
| userMobile | String | 手机号 |
| userEmail | String | 邮箱 |
| q1 ~ q32 | String | 各题答案 |
| createdAt | String | 创建时间，格式 `yyyy-MM-dd HH:mm:ss` |
| updatedAt | String | 更新时间，格式 `yyyy-MM-dd HH:mm:ss` |

### 响应示例

```json
{
  "code": 200,
  "message": "success",
  "data": [
    {
      "id": 1,
      "userName": "张三",
      "userMobile": "13800138000",
      "userEmail": "zhangsan@example.com",
      "q1": "A",
      "q2": "B",
      "q3": "A",
      "q4": "C",
      "q5": "B",
      "q6": "A",
      "q7": "D",
      "q8": "B",
      "q9": "A",
      "q10": "C",
      "q11": "B",
      "q12": "A",
      "q13": "D",
      "q14": "B",
      "q15": "A",
      "q16": "C",
      "q17": "B",
      "q18": "A",
      "q19": "D",
      "q20": "B",
      "q21": "A",
      "q22": "这是一道长文本题的回答内容...",
      "q23": "A",
      "q24": "B",
      "q25": "这是另一道长文本题的回答内容...",
      "q26": "C",
      "q27": "长文本回答...",
      "q28": "A",
      "q29": "B",
      "q30": "长文本回答...",
      "q31": "A",
      "q32": "B",
      "createdAt": "2026-05-19 10:00:00",
      "updatedAt": "2026-05-19 10:00:00"
    }
  ]
}
```

---

## 通用响应结构

| 字段 | 类型 | 说明 |
|---|---|---|
| code | Integer | 状态码，`200` 表示成功 |
| message | String | 提示信息 |
| data | Object/Array/null | 响应数据 |
