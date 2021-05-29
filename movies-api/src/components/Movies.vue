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

    <div class="row">
      <div class="col-sm-12 mt-5">
        <div class="card">
          <div class="row card-body">
            <img class="col-sm-4" src="https://m.media-amazon.com/images/M/MV5BNjM0NTc0NzItM2FlYS00YzEwLWE0YmUtNTA2ZWIzODc2OTgxXkEyXkFqcGdeQXVyNTgwNzIyNzg@._V1_SX300.jpg" alt="sans"/>

            <div class="col-sm-8">
              <h5 class="card-title">Card title</h5>

              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>


              <ul class="list-group list-group-flush">
                <li class="list-group-item">An item</li>
                <li class="list-group-item">A second item</li>
                <li class="list-group-item">A third item</li>
              </ul>

            </div>

            <div class="card-body">
              <a href="#" class="card-link me-3">Card link</a>
              <a href="#" class="btn btn-primary ml-3">Go to IMDB</a>
            </div>
          </div>
        </div>
      </div>
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