# 免责声明

本项目仅供学习交流，禁止用于商业用途

使用该脚本有一定风险(如黑号,封号,权重降低等)，本项目不承担任何责任

## 项目介绍

Boos直聘助手, 皆在减少投递简历的麻烦, 和提高投递简历的效率,技术栈使用VIte + Vue3 + element-plus, 代码由 Vite 打包无加密混淆最小化,开源在 Github 欢迎前来Pr

> 本项目处于积极维护状态
> 24.04.11 后续会加上各个版本的更新内容，并且进行认真测试。最近在优化过程中，不慎将GPT内容发送给了老板而导致了严重的尴尬局面。以此为戒

## 项目预览

[![卡片状态](docs/img/shot_2024-04-14_23-08-03.png)](docs/img/shot_2024-04-14_23-08-03.png)
[![账户配置](docs/img/shot_2024-04-14_23-09-05.png)](docs/img/shot_2024-04-14_23-09-05.png)
[![统计界面](docs/img/shot_2024-04-02_22-25-25.png)](docs/img/shot_2024-04-02_22-25-25.png)
[![配置界面](docs/img/shot_2024-04-02_22-26-54.png)](docs/img/shot_2024-04-02_22-26-54.png)
[![日志界面](docs/img/shot_2024-04-02_22-32-25.png)](docs/img/shot_2024-04-02_22-32-25.png)

## 版本说明

[1+.x.x] 为正式版本,同步github的release版本,不保证稳定性只是功能相对完善

[202x.x.x.alpha]/[0.x.x] 为测试版本,同步github的master分支,自动构建

[README.user.md](README.user.md) 为用户使用说明，重要变更此处不再说明

## 未来计划

- [x] 优化UI去除广告
- [x] 批量投递简历
- 高级筛选
  - [x] 薪资,公司名,工作名,人数,内容简单筛选
  - [ ] 通勤时间
  - [ ] 公司风险评控
  - [x] GPT筛选
- 自动打招呼
  - [x] 模板语言
  - [x] 支持chatGPT,自定义http调用
- GPT赋能
  - [ ] 自动回复聊天
  - [x] 多模型管理
- 额外功能(有时间会写)
  - [x] 暗黑模式
  - [x] 自适应UI适配手机
  - [ ] 黑名单
  - [x] 多账号管理
  - [ ] 聊天屏蔽已读消息
  - [ ] boos消息弹窗

## 相关链接

Github开源地址: <https://github.com/ocyss/boos-helper>

greasyfork地址: <https://greasyfork.org/zh-CN/scripts/491340>

## 参与贡献

> 本项目写的一托,包括文件名,变量名,不完整的注释,解释不到位的help...,如果有更好的命名,功能解释,文件结构优化方案,请直接提交pr,让你的名字出现到贡献者名单中。

1. Fork 本仓库并克隆到本地。
2. 在新分支上进行您的更改：`git checkout -b 您的分支名称`
3. 提交更改：`git commit -am '描述您的更改'`
4. 推送更改到您的 Fork：`git push origin 您的分支名称`
5. 提交 Pull 请求。

- 在开发时server模式会注入脚本,也可能导致跨域问题请禁用以下两个策略
  
  chrome 用户:

  - chrome://flags/#block-insecure-private-network-requests
  - chrome://flags/#private-network-access-respect-preflight-results

  edge 用户:

  - edge://flags/#block-insecure-private-network-requests
  - edge://flags/#private-network-access-respect-preflight-results

## 鸣谢

- <https://github.com/yangfeng20/boss_batch_push>
- <https://github.com/lisonge/vite-plugin-monkey>
- <https://github.com/chatanywhere/GPT_API_free>
  
- <https://uiverse.io/>
- <https://www.runoob.com/manual/mqtt/protocol/MQTT-3.1.1-CN.pdf>
  
## 类似项目

- <https://github.com/Frrrrrrrrank/auto_job__find__chatgpt__rpa>
- <https://github.com/noBaldAaa/find-job>

## 最后

嗯...

## Star 趋势

<a href="https://star-history.com/#ocyss/boos-helper&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=ocyss/boos-helper&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=ocyss/boos-helper&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=ocyss/boos-helper&type=Date" />
 </picture>
</a>