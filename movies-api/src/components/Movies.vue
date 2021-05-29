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

    <!-- <div
      class="row"
      v-if="!movieDetails">
      <div class="col-sm-12 mt-5">
        <div class="card">
          <div class="row card-body welcome-card">
            <div class="col-sm-12">
              <p class="card-text">Welcome 🍿</p>
            </div>
          </div>
        </div>
      </div>
    </div> -->

    <div class="row"
      v-if="movieDetails">
      <div class="col-sm-12 mt-5">
        <div class="card">
          <div class="row card-body">
            <img class="col-sm-4" :src="movieDetails.Poster" alt="sans"/>

            <div class="col-sm-8">
              <h1 class="card-title">{{ movieDetails.Title }}</h1>

              <h6 class="card-text mt-4">{{ movieDetails.Plot }}</h6>
              <div class="card-text">{{ movieDetails.Year }}</div>
              <div class="card-text">{{ movieDetails.Runtime }}</div>
              <div class="card-text">{{ movieDetails.Released }}</div>
              <div class="card-text">{{ movieDetails.Genre }}</div>
              <div class="card-text">{{ movieDetails.Director }}</div>
              <div class="card-text">{{ movieDetails.Writer }}</div>
              <div class="card-text">{{ movieDetails.Actors }}</div>
              <div class="card-text">{{ movieDetails.Language }}</div>
              <div class="card-text">{{ movieDetails.Country }}</div>
              <div class="card-text">{{ movieDetails.Awards }}</div>
              <div class="card-text">{{ movieDetails.BoxOffice }}</div>
              <div class="card-text">{{ movieDetails.Production }}</div>
              <div class="card-text">{{ movieDetails.Awards }}</div>
              <div class="card-text">{{ movieDetails.imdbID }}</div>

              <div class="row">
                <div class="col-sm-4 score-cards"
                  v-for="(rating, index) in movieDetails.Ratings"
                  :key="index">

                  <div class="score-class">
                    <span>{{ rating.Source }}</span>

                    <div>
                      <span v-if="rating.Source === 'Rotten Tomatoes'">🍅</span>

                      {{ rating.Value }}
                    </div>

                  </div>
                </div>
              </div>

              <div class="card-body">
                <a :href="`https://www.imdb.com/title/${movieDetails.imdbID}`" target="_blank" class="btn btn-primary ml-3">Go to IMDB</a>
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

          // this.searchInput = ''
        }
      })
    }
  },

  created () {
    this.searchInput = 'jumanji'
    this.getMovieDetails()
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

  .welcome-card {
    font-size: 50px;
  }

  .score-cards {
    display: flex;
    justify-content: space-evenly;
  }

  .score-class {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    background-color: rgba(255, 255, 0, 0.733);
    border: 2px solid rgb(255, 255, 21);
    padding: 10px;
    width: 200px;
    height: 100px;
    border-radius: 10%;
  }
</style>