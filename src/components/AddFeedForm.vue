<template>
  <section class="add-feed-form">

    <h1>Add Feed</h1>

    <form>
      <input v-model="idToAdd" placeholder="feed id" />
      <button @click.prevent="addFeed">Add Feed</button>
    </form>

  </section>
</template>

<script>
export default {
  name: 'add-feed-form',

  data() {
    return {
      idToAdd: '',
    };
  },

  methods: {
    addFeed() {
      const params = {
        method: 'POST',
      };

      fetch(`http://localhost:3001/feeds/${this.idToAdd}`, params)
        .then(res => console.log(res))
        .catch(err => console.log(err));
    },
  },
};
</script>

<style scoped>
</style>

