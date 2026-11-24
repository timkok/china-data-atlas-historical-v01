# China Data Atlas · 中国数据地图

免费公开访问的中国省级统计数据产品。V0.1 为**历史数据预览**，不是最新统计数据库：10个指标、31个省级地区，统计年度按指标为2011—2020或仅2020。来源为国家统计局《中国统计年鉴2021》。

## 本地运行

需要 Node.js 22+、Python 3.11+。

```sh
npm ci
npm run dev
```

## 可复现数据

```sh
python3 -m pip install -r pipeline/requirements.txt
python3 pipeline/fetch_release.py
python3 pipeline/build.py
python3 pipeline/validate.py --links
npm run build
```

`public/data/atlas.json` 为预计算数据接口，`public/data/{indicator-id}.csv` 为带出处的数据导出，`dictionary.json` 为字典。`data/processed/observations.parquet` 和本地生成的 DuckDB 可供研究使用。原始年鉴不作为本站授权材料重新分发；通过原始官方链接取回并验证SHA256。

`pipeline/extract.py` 和 `ocr.py` 是实验性候选提取流程，**不在发布链路中**。双次OCR一致不能作为统计数据已核验的证明。原始图片候选与待核验数据不进入网站。

## 数据边界

- 人口及城镇化率：2011—2020；收入及消费支出：2014—2020。
- GDP、人均GDP、65岁及以上人口占比、普通本专科在校生、普通高校数、医院病床使用率：仅2020。
- GDP采用原表初步核算数；未合并后续修订。全国GDP缺失，不用省份加总代替。
- 老龄占比按普查表同表分子分母计算；不能用年末人口作为分母。
- 原Excel隐藏小数按单元格官方显示精度处理；原始值与格式保留于导出。
- 香港、澳门、台湾不在本版统计覆盖内。这是统计覆盖说明，不表示地理归属判断。
- 地图暂缓：资源许可、审图及交互修改合规性尚未确认。提供省级排名和地区比较。
- 不启用付费服务或AI模型API。

详见 `docs/research.md`、`docs/source-audit.md`、`docs/quality-report.json` 和 `docs/delivery.md`。
