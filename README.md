# 🐍 leserpent v0.01 Design Spec

### eBPF Control Plane & Visual Orchestration Service

MIT License
Status: Draft v0.01

---

## 0. 定位

leserpent 是：

> control plane / management service

不是：

* CLI wrapper
* runtime
* execution engine

它负责：

* 生成 pipeline spec
* 分发
* 管理
* 可视化
* 审计

---

## 1. 核心原则

1. 不直接操作 kernel
2. 不直接 attach eBPF
3. 所有 execution 委托 gewyvern
4. 必须依赖 runtime capability
5. runtime 权威优先

---

## 2. 部署模型

* ASP.NET Core
* server-first
* 可跨平台部署
* 不建议部署普通客户端

---

## 3. 连接模型

```
leserpent → gewyvern
```

短连接：

* 即时 gRPC

非：

* 长连接 agent 控制

---

## 4. 配对模型

流程：

1. gewyvern 提供 token
2. leserpent 生成密钥对
3. 交换公钥
4. 建立 trust

之后：

* 所有请求签名

---

## 5. Pipeline assembler

用户：

* 不接触 protobuf
* 不写 JSON

UI：

* 组合 pipeline

leserpent：

> 生成 protobuf spec

---

## 6. 能力依赖模型

leserpent：

* 必须读取 gewyvern capability
* 不可假设 runtime 能力

---

## 7. 三态处理

| 状态              | 行为           |
| --------------- | ------------ |
| not supported   | 禁止           |
| risky           | UI提示，不允许远程执行 |
| fully supported | 允许           |

---

## 8. session 管理

leserpent：

* 创建
* 查询
* 停止
* 审计

但：

> 不管理 kernel state

---

## 9. 安全责任

身份：

* user auth
* RBAC
* audit

runtime：

* 不承担

---

## 10. UI 目标

* pipeline 可视化
* session 可视化
* metrics / trace 展示

---

## 11. 不做的事情

* 不做 kernel runtime
* 不做 attach
* 不做 verifier
* 不做 eBPF 编译

