<template>
  <div id="app">
    <add-feed-form :onAdd="fetchFeeds"></add-feed-form>
    <feed-list :feeds="this.feeds"></feed-list>
  </div>
</template>

<script>
import FeedList from './components/FeedList';
import AddFeedForm from './components/AddFeedForm';

export default {
  name: 'app',

  components: {
    FeedList,
    AddFeedForm,
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
      fetch('proxy/feeds')
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
