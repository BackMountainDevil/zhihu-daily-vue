<script>
import axios from 'axios'

export default {
  data() {
    return {
      stories: "",
      top_stories: "",
      story: ""
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:8010/news/latest')
      .then((response) => {
        this.stories = response.data.stories;
        this.top_stories = response.data.top_stories;
        for (var i in this.stories) { // 图片地址外移
          if (this.stories[i].images) {
            this.stories[i].image = this.stories[i].images[0]
          }
        }
      })
      .catch(function (error) {
        console.error(error);
      });
  },
  methods: {
    getContent(id) {
      axios.get("http://127.0.0.1:8010/news/" + id)
        .then((response) => {
          this.story = response.data
          scrollTo(0,0) // 页面滚动到顶部
        })
    }
  }
}
</script>

<template>
  <div class="content" v-if=story>
    <h1>{{ story.title }}</h1>
    <div v-html=story.body></div>
    <a :href=story.share_url>查看原文</a>
  </div>

  <div class="content"  v-if=stories >
    <h1>每日推荐</h1>
    <div v-for="item in stories">
      <div class="left"><img class="image" v-if=item.image :src=item.image /></div>
      <div class="right"><a class="title" @click="getContent(item.id)"> {{ item.title }} - {{ item.hint }}</a></div>
    </div>
  </div>

  <div  class="content" v-if=top_stories>
    <h1>主题日报</h1>
    <div>
      <div v-for="item in top_stories">
        <div class="left"><img class="image" v-if=item.image :src=item.image /></div>
      <div class="right"><a class="title" @click="getContent(item.id)"> {{ item.title }} - {{ item.hint }}</a></div>
      </div>
    </div>
  </div>


</template>

<style>
.image {
  width: 50px;
  height: 50px;
}

.title {
  color: black;
  font-weight: normal;

  border-radius: 5px;
}

.left {
  float: left;
  width: 60px;
  height: 50px;
}

.right {
  height: 60px;
  width: 100%;
  margin-left: 60px;
  margin-top: 5px;
}

.content{
  margin-left: 5%;
  margin-right: 5%;
}
</style>