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
        })
    }
  }
}
</script>

<template>
  <div v-if=stories>
    <h1>每日推荐</h1>
    <div v-for="item in stories">
      <div v-if=item.image> <img :src=item.image /></div>
      <a @click="getContent(item.id)"> {{ item.title }} - {{ item.hint }}</a>
    </div>
  </div>

  <div v-if=top_stories>
    <h1>主题日报</h1>
    <div v-for="item in top_stories">
      <div v-if=item.image> <img :src=item.image /></div>
      <a @click="getContent(item.id)"> {{ item.title }} - {{ item.hint }}</a>
    </div>
  </div>

  <div v-if=story>
    <h1>{{ story.title }}</h1>
    <div v-html=story.body></div>
    <a :href=story.share_url>查看原文</a>
  </div>
</template>
