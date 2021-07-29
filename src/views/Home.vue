<template>
  <div class="home">
    <PlayerAddition msg="Register new player"/>
  </div>
    
</template>

<script>
// @ is an alias to /src
import PlayerAddition from '@/components/PlayerAddition.vue'

export default {
  name: 'Home',
  components: {
    PlayerAddition
  }
}
</script>
