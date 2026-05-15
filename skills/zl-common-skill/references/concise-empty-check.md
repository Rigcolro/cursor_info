# JavaScript/TypeScript 简洁空态判断

在 JavaScript / TypeScript 代码中，对于包含空值的字符串或数值类型的数据，判断空字符串或数值 0 时只需使用 `!value` 即可，禁止使用冗余的长链判断。只有当其他假值在业务上是合法值时，才需要精确判断。

## 核心术语定义与场景约定（消除歧义）

为防止混淆，本规则严格区分以下两种字符串状态：

1. **空字符串 (Empty String)**
   - **定义**：长度为 0 的绝对空字符串，即 `""` 或 `''`。
   - **拦截方式**：使用 `!value` 即可拦截。
   - **场景约定（默认）**：拦截**空字符串**即可。保留并允许用户输入纯空格。此时统一使用 `!value`。

2. **空白字符串 (Blank/Whitespace String)**
   - **定义**：仅包含空格、制表符（Tab）、换行符等空白字符，且长度大于 0 的字符串（例如 `"   "`）。
   - **拦截方式**：`!value` **无法拦截**空白字符串。必须使用 `typeof value === 'string' && value.trim() !== ''` 进行精确判断。
   - **场景约定（特例）**：在表单必填项提交、搜索关键词校验、用户评论输入等典型场景中，纯空格被视为无效输入，必须拦截**空白字符串**。

## 强制规则

- 对于字符串相关类型（如 `string | undefined | null`、`string | undefined`、`string | null` 或纯 `string`），判断空字符串只需使用：`!value`
- **严禁**使用冗余写法：
  - `value !== null && value !== undefined && value !== ''`
  - 包含前置类型判断的冗余组合（如 `typeof value === 'string' && value` 或 `typeof value !== 'string' || !value`）
  - 任何语义等价的多段 null/undefined/空字符串拼接判断
- 能用单一表达式表达意图时，不要拆成多个 `&&` 或 `||` 条件

## 例外规则（必须显式说明意图）

只有当其他假值在业务上是合法值，或业务需要更精确地排除空白字符串时，禁止直接使用 `!value`，必须改为精确判断：

- `0` 是合法值
- `false` 是合法值
- `NaN` 需要和空值分开处理
- 需要排除“空白字符串”（如表单校验场景要求非空白字符串）
- 仅需判断 null/undefined（nullish），不应误伤其他假值

## 注释要求（严格）

当使用“非 `!value`”写法是为了保留某个假值时，必须在附近添加简短注释，说明业务原因（例如“0 为合法值，不能按空处理”）。

## 示例

### 1. 字符串相关类型

适用类型：`string | undefined | null`, `string | undefined`, `string | null`, `string`

```ts
// ❌ 禁止：冗余长链
if (name !== null && name !== undefined && name !== '') {
  saveName(name)
}

// ❌ 禁止：冗余的前置类型判断
if (typeof name === 'string' && name) {
  saveName(name)
}

// ✅ 允许（默认场景）：统一处理 '' / null / undefined 
// 说明：拦截空字符串，允许输入纯空格
if (!name) {
  return
}

// ✅ 允许（表单校验/搜索等场景）：拦截空白字符串
// 说明：纯空格等视为无效输入
if (typeof keyword === 'string' && keyword.trim() !== '') {
  search(keyword)
}
```

### 2. 数值相关类型

适用类型：`number | undefined | null`, `number | undefined`, `number | null`, `number`

```ts
// ❌ 禁止：冗余的前置类型判断
if (typeof count === 'number' && count) {
  saveCount(count)
}

// ✅ 允许：0 视为无效值时，直接使用 !count
if (!count) {
  return
}

// ✅ 允许：0 为合法值时，改为 nullish 判断并写明原因
// 业务约束：count 可为 0，不能按空值处理
if (count == null) {
  return
}
```
