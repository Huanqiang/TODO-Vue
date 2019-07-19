<template>
  <div class="todo-container">
    <Header />
    <Container />
    <Footer />
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
import Header from '@/components/Header.vue';
import Container from '@/components/Container.vue';
import Footer from '@/components/Footer.vue';
export default Vue.extend({
  components: { Header, Container, Footer },
});
</script>
<style lang="scss">
.todo-container {
  width: 500px;
  margin: 0px auto;
}
</style>
