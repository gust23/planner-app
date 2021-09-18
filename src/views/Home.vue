<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <h1 v-if="errorMessage"></h1>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject @done="handleDone" @delete="handleDelete" :project="project" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';
export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      url: 'http://localhost:3000/projects/',
      current: 'all',
      errorMessage: '',
    };
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter((item) => item.complete);
      }
      if (this.current === 'ongoing') {
        return this.projects.filter((item) => !item.complete);
      }
      return this.projects;
    },
  },
  methods: {
    async fetchData() {
      try {
        const res = await fetch(this.url);
        if (!res.ok) {
          throw Error('no data available');
        }
        const data = await res.json();
        return data;
      } catch (error) {
        this.errorMessage = error.message;
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
