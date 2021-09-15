<template>
  <form @submit.prevent="handleEdit">
    <label>Title: </label>
    <input type="text" v-model="title" required />
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>
<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      url: 'http://localhost:3000/projects/',
    };
  },
  methods: {
    async handleEdit() {
      try {
        await fetch(this.url + this.id, {
          method: 'PATCH',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            complete: false,
            title: this.title,
            details: this.details,
          }),
        });
      } catch (error) {
        console.log(error);
      }
      this.$router.push('/');
      this.title = '';
      this.details = '';
    },
  },
  async mounted() {
    const res = await fetch(this.url + this.id);
    const data = await res.json();
    this.title = data.title;
    this.details = data.details;
  },
};
</script>
<style></style>
