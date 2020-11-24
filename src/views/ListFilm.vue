<template>
<div class="newPage">
  <div class="container">
   <h1 class="text-left p-4 ml-5 ">{{film.name}}</h1>

      <img :src="film.photo" class="img-fluid" alt="Responsive image">
    
    <div class="p-4 ml-5 row">
      
      <div class="col-lg-12 text-left pt-4"><b>Description</b>
      <p>{{film.description}}</p>
      </div>

      <div class="col-lg-12 text-left pt-2"><b>Release Data</b>
      <p>{{film.release_date}}</p>
      </div>

      <div class="col-lg-12 text-left pt-2"><b>Rating</b>
      <p>{{film.rating}}</p>
      </div>

      <div class="col-lg-12 text-left pt-2"><b>Ticket Price</b>
      <p>{{film.ticket_price}}</p>
      </div>

      <div class="col-lg-12 text-left pt-2"><b>Country</b>
      <p>{{film.country}}</p>
      </div>

      <div class="col-lg-12 text-left pt-2"><b>Genre</b>
      <p>{{film.genre}}</p>
      </div>

        
    </div>

    </div>

   
     

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

