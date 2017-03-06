<template>
  <div id="app">
    <add-feed-form :onAdd="fetchFeeds"></add-feed-form>
    <feed-list 
      :feeds="this.feeds"
      :onDelete="fetchFeeds"
      :onImport="fetchFeeds"></feed-list>

    <section>
      <h1>Import</h1>
      <button @click.prevent="megaImport">Mega Import!</button>
    </section>
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
      fetch(`${process.env.API}/feeds`)
        .then(res => res.json())
        .then(feeds => (this.feeds = feeds));
    },

    megaImport() {
      fetch(`${process.env.API}/mega_import`, { method: 'POST' })
        .then(res => res.json())
        .then(count => console.log(count));
    },

  },
};
</script>

<style>
button {
  background-color: #0074D9;
  border: none;
  color: #fff;
  border-radius: 0.2em;
}
button.danger {
  background-color: #FF4136;
}
</style>
