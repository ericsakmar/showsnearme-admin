<template>
  <div id="app">
    <feed-list :feeds="this.feeds"></feed-list>
  </div>
</template>

<script>
import FeedList from './components/FeedList';

export default {
  name: 'app',

  components: {
    FeedList,
  },

  data() {
    return {
      feeds: [],
    };
  },

  created() {
    this.fetchFeeds();
  },

  methods: {
    fetchFeeds() {
      fetch('http://localhost:3001/feeds')
        .then(res => res.json())
        .then(feeds => (this.feeds = feeds));
    },
  },
};
</script>

<style>
#app {
}
</style>
