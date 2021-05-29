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

    <div
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
    </div>

    <div class="row"
      v-if="movieDetails">
      <div class="col-sm-12 mt-5">
        <div class="card">
          <div class="row card-body">
            <img class="col-xs-12 col-lg-4" :src="movieDetails.Poster" alt="sans"/>

            <div class="col-xs-12 col-lg-8">
              <h1 class="card-title">{{ movieDetails.Title }}</h1>

              <h5 class="card-text plot mt-4 mb-4">{{ movieDetails.Plot }}</h5>

              <div class="card-text">
                <label>Year: </label>
                {{ movieDetails.Year }}
              </div>

              <div class="card-text">
                <label>Runtime: </label>
                {{ movieDetails.Runtime }}
              </div>

              <div class="card-text">
                <label>Genre: </label>
                {{ movieDetails.Genre }}
              </div>

              <div class="card-text">
                <label>Director: </label>
                {{ movieDetails.Director }}
              </div>

              <div class="card-text">
                <label>Actors: </label>
                {{ movieDetails.Actors }}
              </div>

              <div class="card-text">
                <label>Awards: </label>
                {{ movieDetails.Awards }}
              </div>
              
              <div class="card-text mb-4">
                <label>BoxOffice: </label>
                {{ movieDetails.BoxOffice }}
              </div>

              <div class="row">
                <div class="col-sm-4 score-cards"
                  v-for="(rating, index) in movieDetails.Ratings"
                  :key="index">

                  <div class="score-class">
                    <span><b>{{ rating.Source }}</b></span>

                    <div>
                      <span v-if="rating.Source === 'Rotten Tomatoes'">🍅</span>
                      <span v-else-if="rating.Source === 'Internet Movie Database'"><i class="fab fa-imdb"></i></span>
                      <span v-else>🎬</span>

                      <span class="icon">{{ rating.Value }}</span>
                    </div>
                  </div>
                </div>
              </div>

              <div class="card-body">
                <a :href="`https://www.imdb.com/title/${movieDetails.imdbID}`" target="_blank" class="btn btn-outline-warning imdb-button ml-3">Go to IMDB</a>
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
  },

  created () {
    document.body.style.backgroundImage = "url('https://images.unsplash.com/photo-1489599849927-2ee91cede3ba?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80')"
  }
}
</script>

<style>
  input.form-control::placeholder {
    color: #bebcbca9;
  }

  .welcome-card {
    font-size: 50px;
  }

  h1.card-title {
    font-size: 4.5rem;
  }

  h5.plot {
    text-align: justify;
    padding: 0px 20px 0px 20px
  }

  .score-cards {
    display: flex;
    justify-content: space-evenly;
  }

  .score-class {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    background-color: #e9c51edb;
    border: 2px solid #9a6c6454;
    padding: 10px;
    width: 230px;
    height: 100px;
    border-radius: 10%;
  }

  label {
    font-weight: 700;
  }

  .icon {
    font-weight: 700;
    padding-left: 5px;
  }

  .imdb-button {
    width: 100%;
  }
  .imdb-button:hover {
    box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24), 0 17px 50px 0 rgba(0,0,0,0.19);
  }
</style>