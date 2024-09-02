<template>
  <div>
    <TodoList />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList.vue';
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'HomeView',
  components: {
    HelloWorld,
    TodoList
  }
};
</script>

<style scoped>
/* Globala stilar (om nödvändigt) */
body {
  font-family: Arial, sans-serif;
  background-color: #f9f9f9;
}
</style>