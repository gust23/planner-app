<template>
  <nav class="filter-nav">
    <button :class="{ active: current === 'all' }" @click="updateFilter('all')">View All</button>
    <button :class="{ active: current === 'completed' }" @click="updateFilter('completed')">Completed</button>
    <button :class="{ active: current === 'ongoing' }" @click="updateFilter('ongoing')">Ongoing</button>
  </nav>
</template>
<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(status) {
      this.$emit('filterChange', status);
    },
  },
};
</script>
<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 14px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: coral;
}
</style>
