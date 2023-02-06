<script>
import axios from 'axios'

export default {
  data() {
    return {
      stories: "",
      top_stories: ""
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
  }
}
</script>

<template>
  <div v-if=stories>
    <h1>每日推荐</h1>
    <div v-for="item in stories">
      <div v-if=item.image> <img :src=item.image /></div>
      {{ item.title }} - {{ item.hint }}
    </div>
  </div>

  <div v-if=stories>
    <h1>主题日报</h1>
    <div v-for="item in top_stories">
      <div v-if=item.image> <img :src=item.image /></div>
      {{ item.title }} - {{ item.hint }}
    </div>
  </div>

</template>
