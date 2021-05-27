<template>
  <div class="container">
    Detalhe tarefa

    {{ JSON.stringify(todo) }}
      
  </div>
</template>

<script>
export default {
  name: 'TodoDetails',

  data () {
    return {
      todo: null
    }
  },

  methods: {
    getTodo () {
      this.axios.get('https://gorest.co.in/public-api/todos/' + this.$route.params.todoId).then((response) => {
        this.todo = response.data.data
      })
    }
  },

  created () {
    this.getTodo()
  }
}
</script>

<style>
  .pagination {
    justify-content: center;
  }

  .disabled {
    color: currentColor;
    cursor: not-allowed;
    opacity: 0.5;
    text-decoration: none;
  }
</style>