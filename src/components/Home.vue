<template>
  <div>
    <div>
      <el-card>  
      <el-row>
        <el-col v-bind:key="player" v-for="player in getPlayers" :xs="24" :sm="12" :md="8">
          <el-card> 
            <div> {{ player.name }} </div>
            <div class="box__subtitle"> {{ player.sport }} </div>
            <div class="box__subtitle"> {{ player.views }} views </div>
          </el-card>
        </el-col>

        <el-col v-if="getPlayers.length === 0" :xs="24" :sm="24" :md="24">
          <div class="box box__empty"> No Match Found</div>
        </el-col>

      </el-row> <!-- results -->
      </el-card>
    </div>
 </div> <!-- container -->

</template>

<script>
export default {
  name: 'Home',
  props: {
    filter: {
      type: String
    }
  },
  data: function() {
    return { 
      players: [
        { name: 'Charles Wilson', sport: 'Baseball', views: 312},
        { name: 'Tony Domo', sport: 'Football', views: 23121 },
        { name: 'Rump Baker', sport: 'Basketball', views: 231},
        { name: 'Brad Pitt', sport: 'Acting', views: 443},
        { name: 'Kermit the Frog', sport: 'Frogball', views: 403},
        { name: 'Taylor Swift', sport: 'Singing', views: 8843}
      ]
    }
  },
  computed: {
    getPlayers() {

      var players = this.players.filter(player => {
        return player.name.toLowerCase().includes(this.filter.toLowerCase());
      });

      if (this.sort == 'views') {
        return players.sort(function (a, b) {
          return b.views - a.views;
        });
      } else {
        return players;
      }

    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

.search-wrapper {
  margin: 10px 0;
}

.col-space {
  content: '&nbsp;';
  @media screen and (max-width: 767px) { display: none; }
}

.el-select {
  width: 100%;
}

.filter {
  width: 1110;
  padding: 5px;
  margin: 10px 0px 10px 0px;
  background-color: #ade0e0;
}

</style>
