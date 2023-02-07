# zhihu-daily-vue

[知呼日报](https://daily.zhihu.com/)

## api

https://news-at.zhihu.com/api/4/news/latest

通过 axios 的 get 方法直接向该地址请求内容，会因为 `CORS Missing Allow Origin` 无法获取到理想的内容，curl 和浏览器都可以，这是为什么呢？

### 返回内容例子

每日推荐：https://news-at.zhihu.com/api/4/news/latest

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

文章详情：https://news-at.zhihu.com/api/4/news/9757962

```json
{"body":"<div class......<\/div>","image_hue":"0x364460","publish_time":1675638060,"title":"在一片洼地倒下一湖水，没有任何生物，十年后湖里会有生物吗？","url":"https:\/\/daily.zhihu.com\/story\/9757962","image":"https:\/\/picx.zhimg.com\/v2-ba0a420cf1591a2ae1ffbc7815d67a16.jpg?source=8673f162","share_url":"http:\/\/daily.zhihu.com\/story\/9757962","js":[],"create_time":1675415186,"ga_prefix":"020607","images":["https:\/\/pica.zhimg.com\/v2-97cb5b57f1db4a43d709147243153d88.jpg?source=8673f162"],"type":0,"id":9757962,"css":["http:\/\/news-at.zhihu.com\/css\/news_qa.auto.css?v=4b3e3"]}
```

文章短评：https://news-at.zhihu.com/api/4/story/9757962/short-comments

```json
{
  "comments": [
    {
      "author": "邓谦",
      "content": "鸟类带来鱼卵，这事有依据没有，感觉有点玄幻了",
      "avatar": "https://picx.zhimg.com/d35bf3d2059947021fb3b4871f601c65_l.jpg?source=8673f162",
      "time": 1675684029,
      "id": 34124542,
      "likes": 0
    },
    {
      "author": "海绵宝宝的jio",
      "content": "生命",
      "avatar": "https://picx.zhimg.com/v2-bedfdae220ef750aa713b8ea3c00db7d_l.jpg?source=8673f162",
      "time": 1675657972,
      "id": 34124427,
      "likes": 0
    }
  ]
}
```

https://news-at.zhihu.com/api/4/news/before/20211202

```json
{
  "date": "20211201",
  "stories": [
    {
      "image_hue": "0xb3896b",
      "title": "腐乳到底是怎么发明出来的？",
      "url": "https://daily.zhihu.com/story/9742844",
      "hint": "魏水华 · 9 分钟阅读",
      "ga_prefix": "120107",
      "images": [
        "https://pic3.zhimg.com/v2-3110e23e5923f32a561622df6d976a99.jpg?source=8673f162"
      ],
      "type": 0,
      "id": 9742844
    },
    {
      "image_hue": "0x484848",
      "title": "瞎扯 · 如何正确地吐槽",
      "url": "https://daily.zhihu.com/story/9742853",
      "hint": "VOL.2801",
      "ga_prefix": "120106",
      "images": [
        "https://pica.zhimg.com/v2-30e6c9e919849f76519e57163c0a2872.jpg?source=8673f162"
      ],
      "type": 0,
      "id": 9742853
    }
  ]
}
```

## proxy 代理

代码在 proxy.js

axios 无法通过访问 `https://news-at.zhihu.com/api/4/news/latest`来获取内容，通过访问 `http://127.0.0.1:8010/news/latest` 后则能获取到内容，这就是代理的作用

图片源地址是`https://picx.zhimg.com/v2-9511f5969cde0660261e9abe04ae54d7.jpg?source=8673f162`，代理地址则是 `http://127.0.0.1:8011/img/https://picx.zhimg.com/v2-9511f5969cde0660261e9abe04ae54d7.jpg?source=8673f162`

文章的地址 `https://daily.zhihu.com/story/9757962` 直接 get 也会被跨域请求所禁止，对应的 api `http://news-at.zhihu.com/api/4/news/9757962` 也会被禁止，代理地址是 `http://127.0.0.1:8010/news/9757962`

## Project Setup

```sh
npm install # 安装依赖

node proxy.js # 运行代理
# 打开另一个终端
npm run dev # debug 模式运行

npm run build
```

# 参考

[《Vue.js实战》](https://github.com/icarusion/vue-book)

[Vue 3 doc](https://cn.vuejs.org/guide/introduction.html)

[css左右布局（传统模型、flex、grid）Nice先生的狂想曲 2019.09.30](https://www.jianshu.com/p/1ff30d824cb7)