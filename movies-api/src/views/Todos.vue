<template>
  <div class="container">
    <!-- Criar tarefa -->
    <div class="row">
      <div class="col-lg-6">
        <button
          type="button"
          class="btn btn-outline-primary">

          Criar tarefa
        </button>
      </div>
    </div>

    <!-- Listagem de todos -->
    <div class="row mt-4">
      <div class="col-lg-12">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">ID do Utilizador</th>
              <th scope="col">Descrição</th>
              <th scope="col">Estado</th>
              <th scope="col">Criado a</th>
              <th scope="col">Actualizado a</th>
            </tr>
          </thead>

          <tbody>
            <tr v-if="!hasTodos">
              <td colspan="6">
                Não existem tarefas criadas
              </td>
            </tr>

            <tr
              v-else
              v-for="todo in todos"
              :key="todo.id">
              <td>{{ todo.id }}</td>
              <td>{{ todo.user_id }}</td>
              <td>{{ todo.title }}</td>
              <td>
                <i
                  v-if="todo.completed"
                  class="fas fa-check text-success">
                </i>

                <i
                  v-else
                  class="fas fa-times text-danger">
                </i>
              </td>
              <td>{{ formatDate(todo.created_at) }}</td>
              <td>{{ formatDate(todo.updated_at) }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="row mt-4">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item"><a class="page-link" href="#">Página Anterior</a></li>
          <li class="page-item"><a class="page-link" href="#">1</a></li>
          <li class="page-item"><a class="page-link" href="#">Página Seguinte</a></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'Todos',

  data () {
    return {
      // What the API send me
      maintenanceTodo : {
        id: null,
        userId: null,
        title: '',
        completed: false
      },

      todos: [],

      pagination: {
        total: null,
        pages: null,
        page: 1,
        limit: null
      }
    }
  },

  computed: {
    hasTodos () {
      return this.todos.length > 0
    }
  },

  methods: {
    // fecth da minha API
    getTodos () {
      this.axios.get('https://gorest.co.in/public-api/todos?page=' + this.pagination.page).then((response) => {
        this.todos = response.data.data // Place the answer from our API into our array
      })
    },

    formatDate (date) {
      var splitedDate = date.split('.')[0]

      return moment(splitedDate, 'YYYY-MM-DDTHH:mm:ss').format('DD/MM/YYYY HH:mm:ss') // O formato da data que a API trás e o formato que quero
    }
  },

  created () {
    this.getTodos()
  }
}
</script>

<style>
  .pagination {
    justify-content: center;
  }
</style>
