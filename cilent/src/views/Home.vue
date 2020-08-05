<template>
  <div class="home">
    <div class="name">
      <h1>NBA Player</h1>
    </div>
    <div class="content">
      <v-row>
        <v-col :cols="3" class="pa-4" v-for="(d,index) in data" :key="index">
          <Box :name="d.name" :team="d.team_name"/>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import Box from "../components/box";
export default {
  name: "Home",
  data() {
    return {
      data: null,
    };
  },
  components: {
    Box,
  },
  mounted() {
    axios
      .get("https://nba-players.herokuapp.com/players-stats")
      .then((response) => {
        this.data = response.data.filter(
          (el) => parseInt(el.games_played) >= 48
        );
        this.data.sort();
        this.data.reverse();
        console.log(this.data)
      });
  },
};
</script>
<style scoped>
.name {
  background-color: whitesmoke;
  z-index: 1000;
  height: 50px;
  width: 100%;
  display: flex;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0%;
}
.content {
  margin-top: 50px;
  padding:0px 20px
}
</style>