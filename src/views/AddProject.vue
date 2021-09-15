<template>
  <form @submit.prevent="handleSubmit">
    <label>Title: </label>
    <input type="text" v-model="title" required />
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      title: '',
      details: '',
      url: 'http://localhost:3000/projects/',
    };
  },
  methods: {
    async handleSubmit() {
      let newProject = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      try {
        await fetch(this.url, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(newProject),
        });
      } catch (error) {
        console.log(error);
      }
      this.$router.push('/');
      this.title = '';
      this.details = '';
    },
  },
};
</script>
<style>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #f14f51;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}

input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
  font-size: 24px;
  outline-color: #ddd;
}
textarea {
  border: 1px solid #add;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 130px;
  font-size: 20px;
  resize: none;
  outline-color: #ddd;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #f14f51;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}
</style>
