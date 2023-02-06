<script>
import axios from 'axios'

export default {
  data() {
    return {
      msg: "404"
    }
  },
  mounted() {
    axios.get('http://127.0.0.1:8010/news/latest')
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
