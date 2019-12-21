<template>
  <div class="Container">
    <slot></slot>
  </div>
    
</template>

<script>
export default {
  name: 'Container',
  props: [""],
}
</script>

<style>
.container {
  width: 764px;
  margin: auto;
  box-shadow: 0 0 15px 0 #5f5f5f73;
}
</style>
