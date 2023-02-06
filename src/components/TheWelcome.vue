<script>
import axios from 'axios'

export default {
  data() {
    return {
      msg: "404"
    }
  },
  mounted() {
    axios.get('https://news-at.zhihu.com/api/4/news/latest')
      .then((response) => {
        console.log(response);
        this.msg = response.data;
      })
      .catch(function (error) {
      console.error(error);
      this.msg = response.data;
    });
  }
}
</script>

<template>
{{ msg }}
</template>
