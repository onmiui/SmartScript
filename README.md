# SmartScript

自动跟随上游更新的 mihomo 配置覆写脚本：默认使用 `smart` 智能选点。

本仓库基于 [AIsouler/MyClash](https://github.com/AIsouler/MyClash) 的覆写脚本，由 GitHub Actions 每 30 分钟拉取上游、自动改写后再提交，所以这里始终是最新的一份「Smart 版」。

## 和上游的区别

| | 上游 MyClash | 本仓库 |
| --- | --- | --- |
| 自动选择组类型 | `url-test` | `smart` |
| 自动选择组命名 | 自动选择 | Smart智能选点 |

## 使用方法

把下面的链接作为「覆写脚本」导入支持 JS 脚本覆写的 mihomo 客户端：

```
https://raw.githubusercontent.com/onmiui/SmartScript/main/SmartScript.js
```

这是**覆写脚本**，不是完整配置，仍需你自己的机场订阅，把订阅和本脚本一起用。

## 注意事项

- 必须在客户端里**关闭 DNS 覆写**，否则分流可能不按预期生效。
- Windows 上如需防止 DNS 泄露，关闭「智能多宿主名称解析」，或开启严格路由。
- 本仓库只负责同步与改写，脚本的原始实现归上游所有；上游的配置逻辑、参数说明以其仓库为准。

## 致谢

- [AIsouler/MyClash](https://github.com/AIsouler/MyClash) —— 原始覆写脚本
- [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo) —— 内核
