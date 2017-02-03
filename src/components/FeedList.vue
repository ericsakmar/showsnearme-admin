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
        </tr>
      </thead>
      <tbody>
        <tr v-for="feed in feeds">
          <td>{{feed.name}}</td>
          <td>{{feed.remoteId}}</td>
          <th><button @click.prevent="importFeed(feed.remoteId)">Import</button></th>
        </tr>
      </tbody>
    </table>

  </section>
</template>

<script>
export default {
  name: 'feed-list',
  props: ['feeds'],
  data() {
    return {
      message: '',
    };
  },
  methods: {
    importFeed(id) {
      fetch(`http://localhost:3001/import/${id}`)
        .then(res => res.json())
        .then(res => this.showMessage(`Added ${res.added} shows`));
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
