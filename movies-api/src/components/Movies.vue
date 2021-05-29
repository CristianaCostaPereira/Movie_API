<template>
  <div class="container">
    <div class="input-group flex-nowrap">
      <input
        type="text"
        class="form-control"
        placeholder="Movie Title"
        v-model="searchInput"
        @keyup.enter="getMovieDetails()">

      <span
        class="input-group-text"
        id="addon-wrapping"
        @click="getMovieDetails()">

        <i class="fas fa-search"></i>
      </span>
    </div>

    <div class="row"
      v-if="movieDetails">
      <div class="col-sm-12 mt-5">
        <div class="card">
          <div class="row card-body">
            <img class="col-sm-4" :src="movieDetails.Poster" alt="sans"/>

            <div class="col-sm-8">
              <h5 class="card-title">Card title</h5>

              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>

              <ul class="list-group list-group-flush">
                <li class="list-group-item">An item</li>
                <li class="list-group-item">A second item</li>
                <li class="list-group-item">A third item</li>
              </ul>

              <div class="card-body">
                <a href="#" class="btn btn-primary ml-3">Go to IMDB</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Movies',

  data () {
    return {
      // Don't need to create the object because the API returns all the info in one single JSON object
      movieDetails: null,

      searchInput: '',

      apiKey: '750e29ba'
    }
  },

  methods: {
    getMovieDetails () {
      this.axios.get(`http://www.omdbapi.com/?t=${this.searchInput}&apikey=${this.apiKey}`).then((response) => {
        if (response.data.Error) {
          alert(response.data.Error)

          this.movieDetails = null

        } else {
          this.movieDetails = response.data
        }
      })
    }
  }

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