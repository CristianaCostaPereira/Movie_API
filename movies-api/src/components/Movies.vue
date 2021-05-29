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

<style>
  body {
    background-image: url('https://images.unsplash.com/photo-1562329265-95a6d7a83440?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=964&q=80');
    background-repeat: no-repeat;
    background-size: 100%;
  }
  
  .form-control::placeholder {
    color: #bebcbc;
  }
</style>