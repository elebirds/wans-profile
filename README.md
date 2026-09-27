# Wans personal profile

基于 [Wans 的分组设计](https://github.com/Wans-OS/my-backup/blob/main/clash/config.yaml)维护的个人 Mihomo 模板。此仓库不包含节点凭据或机场订阅链接。

固定导入 URL：

https://raw.githubusercontent.com/elebirds/wans-profile/main/template.yaml

## 初次使用

1. 在 Clash Verge Rev 导入上面的远程配置。
2. 在该订阅的扩展配置中填入自己的 `proxy-providers.MESL`、`proxy-providers.Sakura` 和 `proxies`。节点名使用 `DMIT-hhm`；其他用户需同步修改本地脚本对应名称。
3. 在该订阅的扩展脚本中将 `DMIT 固定` 组的 `proxies` 设置为自己的 DMIT 节点名，追加个人规则和 DNS 例外。
4. 在客户端设置中启用 TUN，并核对 IPv6、端口、局域网访问及最终生效配置。

模板中的两个 inline provider 中的 reject 占位节点和 DMIT 的 REJECT 占位是刻意设计的：尚未填写凭据时，不能当成可用代理订阅。私人覆写仅保存在本机，不提交到本仓库。

## 与上游的区别

- 保留 Wans 的服务分类及七个地区的自动、回退、散列、轮询组。
- 增加 DMIT 固定、MESL 选择、Sakura 选择、下载组。
- 机场地区组只使用 MESL/Sakura；DMIT 不参加机场自动选择。AI 默认固定 DMIT。
- 自动组排除名称中标注五倍的节点，手动选择仍可使用。没有匹配七大地区的节点仍可通过机场选择组访问。
- 关闭局域网代理，不发布控制接口、固定 secret、机场推广地址或个人节点。
- 使用 Fake-IP，区分直连与节点解析；需要本机解析的代理查询经 DMIT DoH。能传递域名的代理请求仍可交由代理服务器解析。
- 不附加虚构 ECS，不重复堆叠 fallback DNS，不统一封锁海外 UDP/443。
- 公共局域网名称交给系统解析；若系统 DNS 已指向本机 Mihomo，必须在本地覆写中将内网名称指向实际路由器/校园解析器，避免回环。
- 国内 Apple/Microsoft CDN 优先直连；下载在 GitHub 等宽泛规则之前分类。AI 规则优先于通用 Google/下载规则。

## 更新与回滚

只编辑 `template.yaml`；不自动追踪上游 main。参考 Wans 更新时，审查分组、规则和 DNS 差异。

发布前：用安装的 Mihomo 对“模板 + 私人覆写”执行 `mihomo -t -d <测试目录> -f <候选文件>`，检查分组引用、节点来源、倍率过滤和 DNS；涉及网络行为时，使用独立端口测试后再切换。不能仅凭 YAML 语法正确就发布。

远程规则集和机场 provider 按各自 interval 更新；模板通过 Clash Verge 的远程订阅更新。它们是不同的更新通道。

每次变更记录到 CHANGELOG，Git 提交保留上一版。回滚时 revert 对应提交并更新订阅。不要随意重命名 `MESL`、`Sakura`、`DMIT 固定` 等本地覆写依赖的名称。

普通订阅 URL 不包含 Clash Verge 的本地扩展或设备设置；换设备需迁移私人覆写。

## 来源

- Wans 源快照 SHA256：`9202a7335a7d7c222e81f33cd88535eafa31081136d2f516fc4d730aa35ca04d`，取得于 2026-09-27。
- 服务规则：[MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)。
- 下载分类：[Sukka Ruleset](https://github.com/SukkaW/Surge)。
- 核心配置语义：[Mihomo 文档](https://wiki.metacubex.one/config/)。

本仓库不保证节点可用性；DNS/TUN/IPv6 的实际行为需要在目标客户端验收。
