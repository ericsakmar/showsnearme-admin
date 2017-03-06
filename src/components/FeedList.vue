<template>
  <section class="feed-list">

    <h1>Feeds</h1>

    <p>{{message}}</p>

    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>ID</th>
          <th></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="feed in feeds">
          <td>{{feed.name}}</td>
          <td>{{feed.remoteId}}</td>
          <th><button @click.prevent="importFeed(feed.remoteId)">Import</button></th>
          <th><button @click.prevent="deleteFeed(feed._id)">Delete</button></th>
        </tr>
      </tbody>
    </table>

  </section>
</template>

<script>
export default {
  name: 'feed-list',
  props: [
    'feeds',
    'onDelete',
  ],

  data() {
    return {
      message: '',
    };
  },

  methods: {

    importFeed(id) {
      fetch(`${process.env.API}/import/${id}`)
        .then(res => res.json())
        .then(res => this.showMessage(`Added ${res.added} shows`));
    },

    deleteFeed(id) {
      const params = { method: 'DELETE' };
      fetch(`${process.env.API}/feeds/${id}`, params)
        .then(() => this.onDelete());
    },

    showMessage(message) {
      this.message = message;
      setTimeout(() => (this.message = ''), 5000);
    },

  },
};
</script>

<style scoped>
</style>
