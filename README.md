# Ave 与 OFT 活动页面

这是可直接修改、预览并推送的独立项目。完整交接说明在上一级 [OFT活动页面交接-Claude.md](../OFT活动页面交接-Claude.md)。

- `index.html`：当前完整活动页，样式、脚本和 Logo 均内嵌，可单独打开或转发。
- `assets/ave-logo.svg`：Ave 彩色图形标志。
- `assets/oft-logo.jpg`：OFT 官方猫头像。
- `LEADERBOARD_API.md`：榜单接口说明；已接入后端公开榜单接口（前 50 名、地址打码）。
- `CNAME`：正式域名 `referral-race01.ave.ai`。

页面已于 11/14 重新设计并上线。奖池卡片展示全部 200 个奖励席位，榜单表格公示前 50 名。三档奖励：1–10 名每人 60 U，11–50 名每人 35 U，51–200 名每人 20 U，合计 5,000 U。

本目录运行 `python3 -m http.server 4173`，访问 http://localhost:4173/ 预览。无需安装依赖或构建。

远程仓库：https://github.com/pc-h5-allpages/oft 。`main` 分支根目录通过 GitHub Pages 发布至 https://referral-race01.ave.ai/ 。本机现有登录可继续用于 Git；项目不包含任何凭据。

交易入口：页面上的“去 Ave 交易 $OFT”按钮（首屏、参与方式、手机底栏）统一跳转 https://ave.ai/token/0x90ba17416946622b37a833580aaebb2512558858-anubis 。顶部和页脚的 Ave Logo 仍链接 https://ave.ai/ 。
