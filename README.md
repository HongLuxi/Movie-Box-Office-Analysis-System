# 实时新闻主题热度分析系统

**Real\-time News Topic Heat Analysis System**
基于多线程爬虫 \+ 文本挖掘 \+ Flask 可视化的新闻主题热度分析实训项目，实现新浪新闻、观察者网新闻数据采集、关键词挖掘、相似度检索与多维度可视化分析。

## 项目简介

本项目为学校课程实训任务，聚焦**实时新闻主题热度分析**，以新浪新闻滚动页为核心数据源，补充爬取观察者网新闻丰富内容类型。
系统实现**多源新闻数据采集→MySQL 存储→文本分词与关键词提取→主题相似度检索→多维度可视化分析**全流程，支持按时间段统计热度、新闻来源分析、媒体质量对比、关键词溯源等功能，可快速完成新闻主题挖掘与热度趋势研判。

## 技术栈

### 爬虫模块

- 多线程爬虫、阻塞式 `requests` 请求

- 数据解析：`BeautifulSoup` \+ 正则表达式

- 爬取平台：新浪新闻滚动页、观察者网新闻页

### 文本分析

- 分词 / 关键词：`jieba`、`TextRank` 算法

- 相似度计算：`TF\-IDF\+余弦相似度`、`平均词向量\+余弦相似度`

- 词向量模型：`Chinese\-Word\-Vectors` 预训练中文词向量

### 可视化与后端

- 后端框架：`Flask`

- 前端展示：`ECharts`、`WordCloud` 词云

### 数据存储

- 数据库：`MySQL`（存储标题、正文、发布时间、来源、浏览量、评论数等）

## 核心功能

1. **新闻主题搜索（核心）**
关键词 / 短语检索，返回 Top30 相似新闻；自动生成主题热度折线图、关键词词云；支持相似度 / 时间 / 浏览量 / 评论数多维度排序。

2. **时间段新闻分析**
自定义时间范围，展示关键词词云、新闻数量柱状图、热度趋势曲线。

3. **新闻来源分布统计**
按新浪、观察者网等来源统计数据占比，可视化展示来源结构。

4. **媒体质量分析**
统计各来源平均浏览量、评论数，对比媒体传播效果与受欢迎程度。

5. **全量新闻总览**
查看库内全部新闻，支持时间筛选，可跳转新闻原网页。

6. **词汇溯源统计**
输入关键词，检索包含该词的全部新闻，用于主题追踪与关键词研究。

## 项目目录结构

```Plain Text
news_heat_analysis/
|── config/                # 全局配置文件夹
│   └── stopwords.txt      # 外置中文停用词文件
├── crawler/                # 多线程爬虫模块
│   ├── sina_spider.py       # 新浪新闻爬虫
│   ├── guanchazhe_spider.py # 观察者网爬虫
│   └── spider_utils.py      # 爬虫工具函数
├── analysis/               # 文本分析模块
│   ├── text_utils.py      # 文本通用工具（加载停用词、分词）
│   ├── jieba_keyword.py     # 分词+TextRank关键词提取
│   ├── tfidf_similarity.py  # TF-IDF相似度计算
│   ├── word2vec_similarity.py # 词向量相似度计算
│   └── word_cloud.py        # 词云生成
├── web/                    # Flask可视化系统
│   ├── app.py               # 项目主入口
│   ├── static/              # 静态资源（ECharts、词云图片）
│   └── templates/           # 前端页面模板
├── db/                     # 数据库配置
│   └── mysql_connect.py     # MySQL连接与操作
├── README.md
└── requirements.txt         # 依赖包清单
```

## 环境配置

### 安装依赖库

```bash
pip install flask requests beautifulsoup4 jieba wordcloud numpy pandas pymysql scikit-learn
```

## 运行步骤

1. 配置 `db/mysql\_connect\.py` 中的 MySQL 数据库连接信息

2. 执行爬虫脚本，采集新闻数据并入库

    ```bash
    python crawler/sina_spider.py
    python crawler/guanchazhe_spider.py
    ```

3. 启动 Flask Web 服务

    ```bash
    cd web
    python app.py
    ```

4. 访问 [http://127\.0\.0\.1:5000](http://127.0.0.1:5000) 进入系统

## 参考项目与资料

1. 观察者网爬虫参考：[https://github\.com/hunter\-lee1/guanchazhe\_spider](https://github.com/hunter-lee1/guanchazhe_spider)

2. 中文预训练词向量：[https://github\.com/Embedding/Chinese\-Word\-Vectors](https://github.com/Embedding/Chinese-Word-Vectors)

## 声明

本项目仅用于**学校课程实训学习**，所有新闻数据版权归原平台所有，请勿用于商业用途。如涉及版权问题，立即删除相关内容。

---

### 操作演示视频（B 站）

待上传：【实时新闻主题热度分析系统 \- 实训项目演示】
