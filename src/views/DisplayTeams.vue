<template>
  
  <div class="about">
    
    <div v-for="team in teams" >
      <div v-for="(player,index) in team" :key="index">
        <h2>{{index}}</h2>
      
        

        <div v-for="(single,index) in player" :key="index">
          <h3>Player number {{index + 1}}</h3>
          
          <p>
          Player name : {{single.name}}<br>
          Player role : {{single.role}}<br>
          Player photo : <img :src="single.preview"> <br>
          <!-- Player image: <img :src="single.image"> -->
          </p>
          <br>
        </div>
      </div>

           
    </div>



  </div>
</template>

<script>


export default {
  name: 'DisplayTeams',
  
  components: {
    
  },


  data () {
    return {      
      teams:{},
    }

  },
  mounted() {
    fetch("http://localhost:3000/teams")
    .then((res)=>res.json())
    .then(Data => this.teams = Data)
    .then(Data => console.log(Data))    
    .catch(err => console.log(err.message))
    
  },

  methods: {

  }
  
}
</script>