<script>
import axios from 'axios';

export default {
  methods: {
    click: () => {
      console.log('log')
    }
  },
  mounted: async () => {
    const url = 'http://127.0.0.1:5000/rss-reader-585ee/us-central1/getRssFead';
    const payload = {
      rssUrlList: [
        "https://hnrss.org/frontpage",
        "https://cprss.s3.amazonaws.com/frontendfoc.us.xml"
      ]
    };
    try {
      const response = await axios.post(url, payload, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded'
        }
      });
      console.log(response)
    } catch (error) {
      console.error(error);
    }
  }
}

</script>

<template>
<div>
  hello world
  <button v-on:click="click">click</button>
</div>
</template>

<style scoped>

</style>
