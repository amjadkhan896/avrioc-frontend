<template>
<div class="newPage">
<div class="container">

<div v-if="films && films.length" class="text-left p-4 mb-4">
  <div v-for="film of films" >
  <div class="card">
  <div class="card-header">
    <router-link v-bind:to="'/list-films/' + film.id" >{{film.name}}</router-link>
  </div>
  <div class="card-body">
    <h5 class="card-title">{{film.rating}}</h5>
    <p class="card-text">{{film.description}}</p>
    <router-link v-bind:to="'/list-films/' + film.id" class="btn btn-primary">Go To Detail</router-link>
  </div>
</div>
</div>
</div>
     
  <ul v-if="errors && errors.length">
    <li v-for="error of errors">
      {{error.message}}
    </li> 
  </ul>
  <div class="p-4 mb-4">
 <b-pagination-nav :link-gen="linkGen" :number-of-pages="noOfPages" v-model="currentPage" align="center"  :limit="perPage" use-router/>
</div>
  
    </div>
</div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      films: [],
      errors: [],
      perPage: 1,
      currentPage: 1,
      noOfPages: null,
    }
  },
  methods: {
    linkGen (pageNum) {
                var fullUrl = this.$route.path+ '?page=' + pageNum;
                return fullUrl;


            },
  },

  created() {
    let ApiUrl = `http://avrioc-backend.test/api/list-films`;
    let queryPage = (this.$route.query &&  this.$route.query.page)? ApiUrl+'?page='+this.$route.query.page: ApiUrl;
    axios.get(queryPage)
    .then(response => {
      console.log(this.$route)
      this.films = response.data.filmsData.data
      this.currentPage = response.data.filmsData.current_page
      this.noOfPages = response.data.filmsData.total
    })
    .catch(e => {
      this.errors.push(e)
    })

    
  },
  computed: {
      rows() {
        return this.films.length
      }
    }
}
</script>

