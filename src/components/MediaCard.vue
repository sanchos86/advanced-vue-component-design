<template>
  <div class="card w-50">
    <div class="card-header" v-if="$slots.header">
      <slot name="header"></slot>
    </div>
    <div class="card-body">
      <slot>
        <p class="card-text">With supporting text below as a natural lead-in to additional content.</p>
      </slot>
    </div>
  </div>
</template>

<script>
  export default {};
</script>

<style scoped>

</style>
