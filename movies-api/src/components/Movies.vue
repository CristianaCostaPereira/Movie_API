<template>
  <div class="container">
    <div class="input-group flex-nowrap">
      <input
        type="text"
        class="form-control"
        placeholder="Movie Title">

      <span
        class="input-group-text"
        id="addon-wrapping">

        <i class="fas fa-search"></i>
      </span>
    </div>
  </div>
</template>

<script>

export default {
  
}
</script>

<style scoped>
  .form-control::placeholder {
    color: #bebcbc;
  }
</style>