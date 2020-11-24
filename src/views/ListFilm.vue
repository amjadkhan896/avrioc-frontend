<template>
<div class="newPage">
<h1> {{film.name}}</h1>

    
      <p><strong>{{film.rating}}</strong></p>
      <p>{{film.description}}</p>
     

</div>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      film: null,
      errors: []
    }
  },

  created() {
    axios.get(`http://avrioc-backend.test/api/list-films/` +  this.$route.params.filmId)
    .then(response => {
      this.film = response.data.filmData
    })
    .catch(e => {
      this.errors.push(e)
    })

    
  }
}
</script>

