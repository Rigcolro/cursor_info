# JavaScript/TypeScript Promise 异步写法

在 JavaScript / TypeScript 代码中，处理 Promise 时默认使用 `async/await`，避免使用 `.then/.catch` 链式写法。

## 强制规则

- Promise 调用优先使用 `await`
- 异常处理优先使用 `try/catch`
- 严禁新增 `.then(...)` / `.catch(...)` 链式写法
- 多个异步步骤需要顺序执行时，用连续 `await` 表达流程

## 例外规则（必须显式说明意图）

以下场景可保留 `.then/.catch`：

- 现有代码局部重构风险过高，且本次任务不涉及该异步链

## 注释要求（严格）

当保留 `.then/.catch` 写法时，必须在附近添加简短注释，说明不能改为 `async/await` 的原因。

## 示例

```ts
// ❌ 禁止：新增 then/catch 链
fetchUser()
  .then(user => saveUser(user))
  .catch(error => handleError(error))

// ✅ 推荐：使用 async/await
try {
  const user = await fetchUser()
  await saveUser(user)
} catch (error) {
  handleError(error)
}
```
