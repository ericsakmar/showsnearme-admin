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
  props: ['onAdd'],

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

      fetch(`${process.env.API}/feeds/${this.idToAdd}`, params)
        .then(() => {
          this.idToAdd = '';
          this.onAdd();
        });
    },
  },
};
</script>

<style scoped>
</style>

