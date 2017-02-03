<template>
  <section class="feed-list">

    <h1>Feeds</h1>

    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>ID</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="feed in feeds">
          <td>{{feed.name}}</td>
          <td>{{feed.remoteId}}</td>
        </tr>
      </tbody>
    </table>

  </section>
</template>

<script>
export default {
  name: 'feed-list',
  props: ['feeds'],
};
</script>

<style scoped>
</style>
