<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <span class="material-icons" :class="{ complete: project.complete }"> edit</span>
        </router-link>

        <span @click="this.$emit('delete', project.id)" :class="{ complete: project.complete }" class="material-icons">
          delete</span
        >
        <span
          @click="this.$emit('done', project.id)"
          :class="{ complete: project.complete }"
          class="material-icons tick"
        >
          done</span
        >
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>
<script>
export default {
  props: ['project'],
  data() {
    return {
      showDetails: false,
    };
  },
  methods: {
    // Now using inline functions
    // deleteProject(id) {
    //   this.$emit('delete', id);
    // },
    // toggleComplete(id) {
    //   this.$emit('done', id);
    // },
  },
};
</script>
<style>
.project {
  margin: 20px auto;
  background-color: white;
  padding: 10px 20px;

  box-shadow: 1px 2px 3px rgba(133, 87, 87, 0.05);
  border-left: 4px solid #e90074;
}

.project.complete {
  border-left: 4px solid #1de9b6;
}
.project.complete .tick {
  color: #1de9b6;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  font-size: 26px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}

.material-icons:hover {
  color: #e90074;
}

.material-icons.complete:hover {
  color: #1de9b6;
}

h3 {
  cursor: pointer;
}
</style>
