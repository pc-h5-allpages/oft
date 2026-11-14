# OFT 榜单接口对接

榜单位于静态活动页 `index.html` 的 `#leaderboard` 区域，已于 2026-11-14 接入后端公开接口。

## 公开榜单接口（页面在用）

```
GET https://h5.phaetd4l.com/campaign/v1/ranking/oft_trade_rank
```

- 钱包地址已打码；无需登录。公示名次由 `data.ranking_limit` 决定（11/14 20:30 前后由 50 改为 200）。
- 18:00 前返回活动时间和空列表；开始后后端每分钟刷新一次，从 2026-11-14 18:00（UTC+8）整段统计。
- 跨域已允许 `https://referral-race01.ave.ai`。页面请求不带 Cookie（`credentials: 'omit'`）。

响应结构（节选）：

```json
{
  "status": 1,
  "msg": "SUCCESS",
  "data": {
    "start_time": "2026-11-14T10:00:00Z",
    "end_time": "2026-11-21T16:00:00Z",
    "ranking_limit": 50,
    "total_trader_count": 63,
    "total_tx_volume": "21500.76",
    "results": [
      { "rank": 1, "creator_address": "0x8851************8fe4", "total_tx_volume": "2982", "total_tx_count": 1 }
    ]
  }
}
```

页面使用的字段：

| 字段 | 用途 |
| --- | --- |
| `status` | 必须为 `1`，否则视为失败 |
| `data.results[].rank` | 1–200 的不重复整数，排名以后端为准，前端不重排 |
| `data.results[].creator_address` | 打码地址，原样展示；手机端缩成前 6 位…后 4 位 |
| `data.results[].total_tx_volume` | 数字字符串，展示为两位小数 U |
| `data.total_trader_count` | 榜单底部“已有 N 个地址参与” |
| `data.total_tx_volume` | 榜单底部“活动总交易量” |

接口不返回快照生成时间，页面“最近刷新”显示的是浏览器成功取到数据的时间。

## 页面行为

- 表格行数跟随 `data.ranking_limit`（取它与返回的最大名次中的较大值，上限 200），无需改页面。不足 200 时，表格下方加一行说明剩余名次奖励及“仅公示前 N 名”；等于 200 时不显示该行。
- 打开页面即请求，此后每 30 秒轮询一次，页面切回前台时立即刷新，也可手动点“刷新榜单”。
- 页面在后台时跳过自动请求；单次请求 10 秒超时；前一次未完成不重复发送。
- 请求失败或数据校验不通过时保留上次成功的数据并提示“刷新失败 · 显示上次结果”；返回空列表时显示“活动尚未开始”或“暂无排名”。

## 结算数据

结算用的完整 CSV（地址不打码，含买卖拆分、guid、设备号）由后端单独提供，需要口令访问。**该接口含用户数据，地址和口令不得写进本页面、仓库或任何公开渠道。**

## 修改接口地址

若后端更换地址，改 `index.html` 榜单脚本顶部的 `LEADERBOARD_API_URL` 即可；公示名次变化无需改页面；接口缺 `ranking_limit` 时按 `DEFAULT_PUBLIC_RANKS`（50）处理。
