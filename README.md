# Actual - LazyCat App

[Actual Budget](https://github.com/actualbudget/actual)（本地优先的个人财务管理应用）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`actualbudget/actual-server` 镜像经 `docker.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（26.x 日期式版本同样满足 semver），发现新版本自动构建发布。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。

## 说明

- 单容器（Node.js），全部数据（预算文件 + 账号库）在 `/lzcapp/var/actual:/data`
- **登录方式限定为密码**（`ACTUAL_LOGIN_METHOD=password`）：首次访问创建管理员账号；`header` 自动登录在反向代理场景有安全风险已禁用，`openid` 需要外部 IdP 未启用
- `ACTUAL_TRUSTED_PROXIES` 已配置内网段，限流取真实客户端 IP
- 健康检查 `/`（node fetch，与镜像内一致）

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 许可

MIT（上游）
