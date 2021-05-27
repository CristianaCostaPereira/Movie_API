<template>
  <div class="container">
    <!-- <pre>
      {{JSON.stringify(todo)}}
    </pre> -->

    <div class="row mt-4">
      <div class="col-lg-12">
        <table class="table table-striped">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">ID do Utilizador</th>
              <th scope="col">Descrição</th>
              <th scope="col">Estado</th>
              <th scope="col">Criado a</th>
              <th scope="col">Actualizado a</th>
              <th></th>
            </tr>
          </thead>

          <tbody>
            <tr v-if="todo">
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

              <td>
                <button
                  @click="openEditTodoModal(todo)"
                  type="button"
                  class="btn btn-outline-primary custom-button">

                  <i
                    class="fas fa-pencil-alt">
                  </i>
                </button>


                <button
                  @click="removeTodo()"
                  type="button"
                  class="btn btn-outline-danger custom-button">

                  <i
                    class="fas fa-trash">
                  </i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'TodoDetails',

  data () {
    return {
      id: this.$route.params.todoId,
      todo: null // What  we get from the server
    }
  },

  methods: {
    getTodo () {
      this.axios.get('https://gorest.co.in/public-api/todos/' + this.id).then((response) => {
        this.todo = response.data.data
      })
    },

    formatDate (date) {
      var splitedDate = date.split('.')[0]

      return moment(splitedDate, 'YYYY-MM-DDTHH:mm:ss').format('DD/MM/YYYY HH:mm:ss') // O formato da data que a API trás e o formato que quero
    },

     removeTodo () {
      // don't need to pass an argument because I have scope using this.id that we get from our route/URL

      this.axios.delete('https://gorest.co.in/public-api/todos/' + this.id,
      {
        headers: {
          Authorization: 'Bearer 19cba85ee0aae784b1ebd27da60e9fda8750deaa140b5da0411cbcefc2f2a2c3'
        }
      }).then((response) => {
        if (response.data.code === 204) {
          this.$router.push({ name: 'Todos' }) // to redirect after delete successfully

        } else {
          alert(response.data.data.message)
        }
      })
    },
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

  .custom-button {
    border-radius: 50%;
    margin-right: 5px;
  }
</style>