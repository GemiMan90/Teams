<template>
  
  <div class="about">
    
    <div v-for="team in teams" >
      <!-- <h2 > Players in team {{team}} :</h2> -->
      <div v-for="player in team">
        {{Object.keys(team)}}
        

        <div v-for="single in player">
          <p>
          {{Object.keys(team)[0]}}  
          Player name : {{single.name}}<br>
          Player role : {{single.role}}<br>
          Player photo : {{single.photo}}<br>
          </p>
        </div>
      </div>

           
    </div>



  </div>
</template>

<script>

import HelloWorld from '@/components/HelloWorld.vue'
import team1 from '@/components/HelloWorld.vue';
import team2 from '@/components/HelloWorld.vue';


export default {
  name: 'Home',
  
  components: {
    HelloWorld
  },

  //props:['team1','team2'],

  data () {
    return {
      //player:{name:"",role:""},
      //playerTwo:{name:"",role:""},



      teams:{},
      Pindex:0
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
    AddPlayer(player){
      player.name=this.name,
      player.role=this.role,
      team1.push(player)
      console.log(player)
    },
    updateTeamOne(Team1){
      this.team1 = Team1
    },
    updateTeamTwo(Team2){
      this.team2 = Team2
    },

  }
  
}
</script>