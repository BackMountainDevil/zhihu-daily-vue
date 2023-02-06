# zhihu-daily-vue

[知呼日报](https://daily.zhihu.com/)

## api

https://news-at.zhihu.com/api/4/news/latest

通过 axios 的 get 方法直接向该地址请求内容，会因为 `CORS Missing Allow Origin` 无法获取到理想的内容，curl 和浏览器都可以，这是为什么呢？

### 返回内容例子

```json
{
  "date": "20230206",
  "stories": [
    {
      "image_hue": "0x364460",
      "title": "在一片洼地倒下一湖水，没有任何生物，十年后湖里会有生物吗？",
      "url": "https://daily.zhihu.com/story/9757962",
      "hint": "瞻云 · 2 分钟阅读",
      "ga_prefix": "020607",
      "images": [
        "https://pica.zhimg.com/v2-97cb5b57f1db4a43d709147243153d88.jpg?source=8673f162"
      ],
      "type": 0,
      "id": 9757962
    },
    {
      "image_hue": "0xa18170",
      "title": "为什么今山东简称「鲁」而不是「齐」？",
      "url": "https://daily.zhihu.com/story/9757939",
      "hint": "哈蟆 · 1 分钟阅读",
      "ga_prefix": "020607",
      "images": [
        "https://picx.zhimg.com/v2-93853773f991bdb1b656c5772cf3b921.jpg?source=8673f162"
      ],
      "type": 0,
      "id": 9757939
    }
  ],
  "top_stories": [
    {
      "image_hue": "0x364460",
      "hint": "作者 / 瞻云",
      "url": "https://daily.zhihu.com/story/9757962",
      "image": "https://picx.zhimg.com/v2-ba0a420cf1591a2ae1ffbc7815d67a16.jpg?source=8673f162",
      "title": "在一片洼地倒下一湖水，没有任何生物，十年后湖里会有生物吗？",
      "ga_prefix": "020607",
      "type": 0,
      "id": 9757962
    },
    {
      "image_hue": "0x57473d",
      "hint": "作者 / 马拓",
      "url": "https://daily.zhihu.com/story/9757933",
      "image": "https://pica.zhimg.com/v2-35add9bd77db30fba660e303baaf1441.jpg?source=8673f162",
      "title": "小事 · 你手机里最舍不得删的那张照片有什么故事?",
      "ga_prefix": "020507",
      "type": 0,
      "id": 9757933
    }
  ]
}
```

## proxy 代理

代码在 proxy.js

axios 无法通过访问 `https://news-at.zhihu.com/api/4/news/latest`来获取内容，通过访问 `http://127.0.0.1:8010/news/latest` 后则能获取到内容，这就是代理的作用

## Project Setup

```sh
npm install # 安装依赖

node proxy.js # 运行代理

npm run dev # debug 模式运行

npm run build
```
