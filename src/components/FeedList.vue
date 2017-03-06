<template>
  <section class="feed-list">

    <h1>Feeds</h1>

    <p>{{message}}</p>

    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Last Import</th>
          <th class="number">Count</th>
          <th></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="feed in feeds">
          <td>{{feed.name}}</td>
          <td>{{feed.lastImport && formatDate(feed.lastImport.date)}}</td>
          <td class="number">{{feed.lastImport && feed.lastImport.count}}</td>
          <th><button @click.prevent="importFeed(feed.remoteId)">Import</button></th>
          <th><button @click.prevent="deleteFeed(feed._id)" class="danger">Delete</button></th>
        </tr>
      </tbody>
    </table>

  </section>
</template>

<script>
import moment from 'moment';

export default {
  name: 'feed-list',
  props: [
    'feeds',
    'onDelete',
    'onImport',
  ],

  data() {
    return {
      message: '',
    };
  },

  methods: {

    importFeed(id) {
      fetch(`${process.env.API}/import/${id}`)
        .then(() => this.onImport());
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

    formatDate(date) {
      return moment(date).format('YYYY-DD-MM [at] hh:mm a');
    },

  },
};
</script>

<style scoped>
tr:hover {
  background-color: #ffd;
}
th {
  text-align: left;
}
.number {
  text-align: right;
}
</style>
