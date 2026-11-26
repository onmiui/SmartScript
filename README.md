# SmartScript

自动跟随上游更新的 mihomo 配置覆写脚本：默认使用 `smart` 智能选点，默认精简掉一批分流组。

本仓库基于 [AIsouler/MyClash](https://github.com/AIsouler/MyClash) 的覆写脚本，由 GitHub Actions 每 30 分钟拉取上游、自动改写后再提交，所以这里始终是最新的一份「Smart 版」。

## 和上游的区别

| | 上游 MyClash | 本仓库 |
| --- | --- | --- |
| 文件头 | AIsouler 署名 | onmiui 署名，并注明改编自上游 |
| 自动选择组类型 | `url-test` | `smart` |
| 自动选择组命名 | 自动选择 | Smart智能选点 |
| 默认分流组 | 全部开启 | 13 个默认关闭（见下文） |
| 更新方式 | 手动维护 | 每 30 分钟自动同步 |

## 使用方法

把下面的链接作为「覆写脚本」导入支持 JS 脚本覆写的 mihomo 客户端：

```
https://raw.githubusercontent.com/onmiui/SmartScript/main/SmartScript.js
```

- 上游作者主推 [Bettbox](https://github.com/appshubcc/Bettbox)，可图形化管理覆写脚本。
- 这是**覆写脚本**，不是完整配置，仍需你自己的机场订阅，把订阅和本脚本一起用。

## 默认关闭的分流组

```
YouTube  Microsoft  Apple     Twitter  Line
Netflix  Emby       PikPak    Spotify  PayPal
Patreon  EHentai    AdBlock
```

- **Bettbox**：脚本里声明了 `Compatible_With_Bettbox`，界面仍会列出这些开关，随时可以重新打开。
- **其它客户端**：配置里不会生成对应的策略组和分流规则，想用得改脚本里的 `DISABLED_OPTIONS`。

关闭后策略组和规则是一起跳过的，不会留下指向不存在策略组的规则。

## 自动同步做了什么

触发方式：定时（每小时 `:17`、`:47`）或手动 `workflow_dispatch`。

每次同步的步骤：

1. 拉取上游 `Script/mihomoScript.js`
2. 用本仓库的文件头替换上游头部注释（保留署名与改编声明）
3. 把 `urlTestBaseOption` 的 `url-test` 类型换成 `smart`
4. 把「自动选择」相关命名统一改成「Smart智能选点」
5. 把 `DISABLED_OPTIONS` 里的 13 个开关默认置为 `false`
6. 写回根目录 `SmartScript.js`，有变化才提交

上游若调整了脚本结构、导致任一替换匹配不到，工作流会直接报错停止，不会提交半成品。

## 自定义

- **恢复某个分流组默认开启**：删掉工作流里 `DISABLED_OPTIONS` 对应那一项。
- **改文件头或署名**：改工作流里的 `HEADER_LINES`。
- **改同步频率**：改 `cron`（注意 GitHub Actions 的定时任务在高峰期可能延迟）。

## 注意事项

- 必须在客户端里**关闭 DNS 覆写**，否则分流可能不按预期生效。
- Windows 上如需防止 DNS 泄露，关闭「智能多宿主名称解析」，或开启严格路由。
- 本仓库只负责同步与改写，脚本的原始实现归上游所有；上游的配置逻辑、参数说明以其仓库为准。

## 致谢

- [AIsouler/MyClash](https://github.com/AIsouler/MyClash) —— 原始覆写脚本
- [appshubcc/Bettbox](https://github.com/appshubcc/Bettbox) —— 上游推荐的客户端
- [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo) —— 内核
