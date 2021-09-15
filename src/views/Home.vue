<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject @done="handleDone" @delete="handleDelete" :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
export default {
  name: 'Home',
  components: { SingleProject },
  data() {
    return {
      projects: [],
      url: 'http://localhost:3000/projects/',
    };
  },
  methods: {
    async fetchData() {
      try {
        const res = await fetch(this.url);
        const data = await res.json();
        return data;
      } catch (error) {
        console.log(error.message);
      }
    },
    async handleDelete(id) {
      const res = await fetch(`${this.url}/` + id, {
        method: 'DELETE',
      });
      res.status === 200
        ? (this.projects = this.projects.filter((item) => item.id != id))
        : alert('Error deleting project');
    },
    async handleDone(id) {
      await fetch(`${this.url}/` + id, {
        method: 'PATCH',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify({ complete: !this.projects.complete }),
      });
      let bvalue = this.projects.find((item) => {
        return item.id === id;
      });
      bvalue.complete = !bvalue.complete;
      this.projects.complete = bvalue.complete;
      console.log(this.projects.complete, id);
    },
  },
  async mounted() {
    this.projects = await this.fetchData();
  },
};
</script>
