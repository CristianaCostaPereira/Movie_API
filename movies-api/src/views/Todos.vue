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
            <tr>
              <th scope="row">1</th>
              <td>Mark</td>
              <td>Otto</td>
              <td>@mdo</td>
              <td>@mdo</td>
              <td>@mdo</td>
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
export default {
  name: 'Todos',

  data () {
    return {
      maintenanceTodo : {
        id: null,
        userId: null,
        title: '',
        completed: false
      }

    }
  }
}
</script>

<style>
  .pagination {
    justify-content: center;
  }
</style>
