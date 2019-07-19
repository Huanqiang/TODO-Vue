<template>
  <div class="info">
  <p>Double-click to edit a todo</p>
  <p>Created by <a href="#">petehunt</a></p>
  <p>Part of <a href="https://www.todomvc.com">TodoMVC</a></p>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
@Component
export default class Footer extends Vue {}
</script>
<style lang="scss">
.info {
  font-size: 9px;
  color: #bfbfbf;
  text-align: center;
}

.info p {
  margin: 4px;
}

.info a:link {
  text-decoration: none;
  color: grey;
}

.info a:visited {
  text-decoration: none;
  color: grey;
}
</style>

