# Google Flights 爬虫工具

[![推广](https://github.com/bright-cn/Awesome-Web-Scraping/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner%20CN.png)](https://www.bright.cn/products/web-scraper/google-flights)

此代码仓库提供两种从 Google Flights 提取航班数据的方式：

1. <strong>免费 Google Flights 抓取工具：</strong>适合小规模数据提取
2. <strong>Google Flights 爬虫工具 API：</strong>专为大规模实时数据提取而设计，请求次数不限。它是 Bright Data [SERP 抓取 API](https://www.bright.cn/products/serp-api) 的一部分。


## 目录
2. [免费爬虫工具](#免费爬虫工具)
   - [设置要求](#设置要求)
   - [快速开始](#快速开始)
   - [输出示例](#输出示例)
   - [限制](#限制)
3. [Google Flights 爬虫工具 API](#google-flights-爬虫工具-api)
   - [主要功能](#主要功能)
   - [前提条件](#前提条件)
   - [直接访问 API](#直接访问-api)
   - [原生代理访问](#原生代理访问)
4. [其他参数](#其他参数)
   - [本地化参数](#本地化参数)
   - [货币参数](#货币参数)
5. [支持与资源](#支持与资源)

## 免费爬虫工具
用于从 Google Flights 提取有限数据的快捷简易抓取工具。

<img width="800" alt="google-flights-scraper" src="https://github.com/bright-cn/google-flights-api/blob/main/images/424383720-44ae10b1-4974-497e-9a7c-c1a762614f0e.png" />

### 设置要求
- [Python 3.9+](https://www.python.org/downloads/)
- 用于浏览器自动化的 [Playwright](https://playwright.dev/)

```bash
pip install playwright
playwright install chromium
```

> **刚接触网页爬虫？** 探索我们的 [Python 网页爬虫入门指南](https://www.bright.cn/blog/how-tos/web-scraping-with-python)
>

### 快速开始
1. 打开 [google-flights-scraper.py](https://github.com/bright-cn/google-flights-api/blob/main/google-flights-scraper/google-flights-scraper.py)
2. 更新以下变量：
    - `url`：粘贴 Google Flights URL（通常包含 `tfs`）。
3. 运行脚本。

💡 专业提示：设置 `HEADLESS = False`，以降低被 Google 反抓取措施检测到的概率。

### 输出示例
```json
{
  "airline": "Emirates",
  "departure_time": "4:15 AM",
  "arrival_time": "2:00 PM",
  "duration": "22 hr 15 min",
  "stops": "1 stop in DXB",
  "price": "$1,139",
  "co2_emissions": "1,092 kg CO2e",
  "emissions_variation": "+6% emissions"
}
```

👉  [查看完整输出示例](https://github.com/bright-cn/google-flights-api/blob/main/google-flights-results/flight_results.json)


### 限制
免费爬虫工具存在以下限制：
- IP 被封禁的风险较高
- 请求量有限
- 频繁出现 CAPTCHA
- 不适合可靠的生产环境使用

如果需要不受这些限制且稳定、可扩展的抓取方案，请考虑使用下方 Bright Data 的专用 API。👇

## Google Flights 爬虫工具 API
[Bright Data 的 Google Flights 爬虫工具 API](https://www.bright.cn/products/web-scraper/google-flights) 已集成到 [SERP 抓取 API](https://www.bright.cn/products/serp-api) 中，并利用我们庞大的[代理网络](https://www.bright.cn/proxy-types)，大规模实时提取价格、时刻表和航空公司详情等航班数据，同时避免 CAPTCHA 和 IP 封禁。

### 主要功能

- <strong>全球精准度：</strong>针对特定位置提供定制结果
- <strong>按成功请求付费：</strong>仅为成功的请求付费
- <strong>实时数据：</strong>数秒内获取最新航班数据
- <strong>无限扩展能力：</strong>轻松处理大规模抓取任务
- <strong>经济高效：</strong>无需搭建昂贵的基础设施
- <strong>性能可靠：</strong>内置反封禁技术
- <strong>全天候专家支持：</strong>随时为你提供帮助

### 前提条件

1. [创建 Bright Data 账户](https://www.bright.cn/)（新用户可获得 5 美元赠金）。
2. 生成你的 [API 密钥](https://docs.brightdata.com/general/account/api-token)。
3. 按照我们的[分步指南](https://github.com/bright-cn/google-flights-api/blob/main/setup-serp-api-guide.md)配置搜索引擎 API 并设置凭据。

### 直接访问 API

直接向 API 端点发出请求。

**cURL 示例：**

```bash
curl https://api.brightdata.com/request \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer API_TOKEN" \
  -d '{
        "zone": "ZONE_NAME",
        "url": "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg",
        "format": "raw"
      }'
```

**Python 示例：**

```python
import requests

url = "https://api.brightdata.com/request"
headers = {"Content-Type": "application/json", "Authorization": "Bearer API_TOKEN"}
payload = {
    "zone": "ZONE_NAME",
    "url": "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg",
    "format": "raw",
}

response = requests.post(url, headers=headers, json=payload)

with open("google-flights-data.html", "w", encoding="utf-8") as file:
    file.write(response.text)
print("HTML response saved to 'google-flights-data.html'.")
```

### 原生代理访问

或者，使用 Bright Data 的代理路由方式。

**cURL 示例：**

```bash
curl -i \
  --proxy brd.superproxy.io:33335 \
  --proxy-user "brd-customer-<customer-id>-zone-<zone-name>:<zone-password>" \
  -k \
  "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg"
```

**Python 示例：**

```python
import requests
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

host = "brd.superproxy.io"
port = 33335
username = "brd-customer-<customer-id>-zone-<zone-name>"
password = "<zone-password>"
proxy_url = f"http://{username}:{password}@{host}:{port}"

proxies = {"http": proxy_url, "https": proxy_url}
url = "https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDREVMcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg"
response = requests.get(url, proxies=proxies, verify=False)

with open("google-flights-data.html", "w", encoding="utf-8") as file:
    file.write(response.text)

print("Response saved to 'google-flights-data.html'.")
```

👉 查看[完整 HTML 输出](https://github.com/bright-cn/google-flights-api/blob/main/google-flights-api-output/google-flights-data.html)。

<strong>注意：</strong>用于生产环境时，请按照 [SSL 证书指南](https://docs.brightdata.com/general/account/ssl-certificate)加载 Bright Data 的 SSL 证书。


## 其他参数
使用以下可选参数微调 Google Flights 数据提取。

### 本地化参数
<img width="800" alt="bright-data-google-flights-api-localization" src="https://github.com/bright-cn/google-flights-api/blob/main/images/424454961-e77f10c9-8e44-46aa-be3d-64c756741479.png" />

根据位置和语言自定义搜索结果：

| 参数 | 说明 | 示例 |
| --- | --- | --- |
| gl | 两位字母国家/地区代码 | `gl=us`（美国） |
| hl | 两位字母语言代码 | `hl=en`（英语） |


<strong>示例：</strong>以法语搜索从巴黎飞往伦敦的航班：

```bash
curl --proxy brd.superproxy.io:33335 --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
"https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDQ0RHcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg&hl=fr&gl=fr"
```

### 货币参数

<img width="800" alt="bright-data-google-flights-api-currency" src="https://github.com/bright-cn/google-flights-api/blob/main/images/424820088-c571e99f-b854-449e-abc2-60149611ad5b.png" />

使用 `curr` 参数定义返回价格所采用的货币。

<strong>示例：</strong>以美元返回价格。

```bash
curl --proxy brd.superproxy.io:33335 --proxy-user brd-customer-<customer-id>-zone-<zone-name>:<zone-password> \
"https://www.google.com/travel/flights/search?tfs=CBwQAhojEgoyMDI1LTA0LTAxagcIARIDQ0RHcgwIAxIIL20vMDRqcGxAAUgBcAGCAQsI____________AZgBAg&hl=fr&gl=fr&curr=USD"
```

## 支持与资源

- **文档：**[搜索引擎 API 文档](https://docs.brightdata.com/scraping-automation/serp-api/)
- **相关 API：**[网络解锁器 API](https://github.com/bright-cn/web-unlocker-api)、[搜索引擎 API](https://github.com/bright-cn/serp-api)、[Google 搜索 API](https://github.com/bright-cn/google-search-api)、[Google 新闻爬虫工具](https://github.com/bright-cn/Google-News-Scraper)、[Google Trends API](https://github.com/bright-cn/google-trends-api)、[Google 评论 API](https://github.com/bright-cn/google-reviews-api)、[Google 酒店 API](https://github.com/bright-cn/google-hotels-api)
- **Google 抓取教程：**
    - [如何抓取 Google Flights](https://www.bright.cn/blog/web-data/how-to-scrape-google-flights)
    - [如何抓取 Google 搜索结果](https://www.bright.cn/blog/web-data/scraping-google-with-python)
    - [如何抓取 Google 地图](https://www.bright.cn/blog/web-data/how-to-scrape-google-maps)
- **使用场景：**
    - [SEO 与 SERP 跟踪](https://www.bright.cn/use-cases/serp-tracking)
    - [旅游行业数据](https://www.bright.cn/use-cases/travel)
- **延伸阅读：**[最佳搜索引擎 API](https://www.bright.cn/blog/web-data/best-serp-apis)
- **联系支持团队：**[support@brightdata.com](mailto:support@brightdata.com)
