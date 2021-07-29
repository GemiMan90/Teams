<template>
<div>
  <h1>{{ msg }}</h1>
  <form >
      <p>Player name: <input v-model="playerName" type="text"></p>
      <p>Player role: 
        <select v-model="playerRole">
        <option value="Tank">Tank</option>
        <option value="DPS">DPS</option>
      </select>
      </p>

        <div class="form-group">
          <label for="my-file">Select Image: </label>
          <input type="file" accept="image/*" @change="previewImage" class="form-control-file" id="my-file">
    
          <div class="border p-2 mt-3">
            <p>Preview Here:</p>
            <template v-if="preview">
              <img :src="preview" class="img-fluid" />
              <p class="mb-0">file name: {{ image.name }}</p>
              <p class="mb-0">size: {{ image.size/1024 }}KB</p>
               </template>
          </div>
        </div>
            <button @click="addTeamOne">Add player to team 1</button>
            <button @click="addTeamTwo">Add player to team 2</button>
            <button @click="saveTeams">Register teams</button>
    </form> 
  </div>

<div class='display' id="display">
    <p> Player name: {{playerName}}</p>
    <p> Player role: {{playerRole}}</p>
</div>
{{team1}}
{{team2}}
<p>
{{teams}}
</p>



</template>

<script>

const axios = require('axios')


export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data () {
    return{
    playerName:'Gemi',
    playerRole:"Tank",
    preview: null,
    image: null,
    team1: [],
    team2: [],
    teams: {"teamOne":null,"teamTwo":null}
  
    }
  },

  methods: {

    addTeamOne(e) {
      console.log(this.playerName,this.playerRole,this.preview,this.image);
      this.team1.push({name:this.playerName,role:this.playerRole,preview:this.preview,image:this.image})
      this.teams.teamOne = this.team1
      console.log(this.team1)

    },
    addTeamTwo(e) {
      console.log(this.playerName,this.playerRole,this.preview,this.image);
      this.team2.push({name:this.playerName,role:this.playerRole,preview:this.preview,image:this.image})
      this.teams.teamTwo = this.team2
      console.log(this.team2)
    },

    saveTeams() {
    axios
    .post('http://localhost:3000/teams', {teams:this.teams
      })
    .then(res => {
        console.log(`statusCode: ${res.statusCode}`)
        console.log(res)
      })
    .catch(error => {
        console.error(error)
      })

    },

    previewImage: function(event) {
      var input = event.target;
      if (input.files) {
        var reader = new FileReader();
        reader.onload = (e) => {
          this.preview = e.target.result;
        }
        this.image=input.files[0];
        reader.readAsDataURL(input.files[0]);
      }
    },
   
    reset: function() {
      this.image = null;
      this.preview = null;
    },
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
