<script>
import axios from 'axios';
import Card from './components/Card.vue'

export default {
  components: {
    Card,
  },
  data() {
    return {
      rawList: [],
    }
  },
  mounted: async function() {
    const url = 'http://127.0.0.1:5000/rss-reader-585ee/us-central1/getRssFeed';
    const payload = {
      rssUrlList: [
        "https://hnrss.org/frontpage",
        "https://cprss.s3.amazonaws.com/frontendfoc.us.xml"
      ]
    };
    try {
      const response = await axios.post(url, payload, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        }
      });
      this.rawList = response.data;
    } catch (error) {
      console.error(error);
    }
  },
  computed: {
    list() {
      const result = [];
      this.rawList.forEach((data) => {
        const source = data.elements.find(item => item.name === 'title');
        const subList = data.elements
          .filter(item => item.name === 'item')
          .map(item => {
            const title = item.elements.find(ele => ele.name === 'title').elements[0];
            const pubDate = item.elements.find(ele => ele.name === 'pubDate').elements[0].text;
            const link = item.elements.find(ele => ele.name === 'link').elements[0].text;
            return {
              title: title[title.type],
              pubDate,
              link,
              origin: source.elements[0].text,
          }});
        result.push(...subList)
      })
      return result;
    }
  }
}

</script>

<template>
<div>
  <ul>
   <Card v-for="item in list" :item="item" />
  </ul>
</div>
</template>

<style scoped>
div {
  max-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

ul {
  list-style: none;
  overflow: scroll;
  max-height: 100vh;
}
</style>
