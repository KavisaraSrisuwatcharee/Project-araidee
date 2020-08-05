<template>
  <v-card style="text-align:center; font-size:1em; font-weight:bold;" width="100%" class="pa-4">
    <v-row>
      <v-col :cols="12">
        <img width="100%" :src="photo" />
      </v-col>
      <v-col :cols="12">NAME: {{name}}</v-col>
      <v-col :cols="12">TEAM: {{team}}</v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  props: ["name", "team"],
  data() {
    return {
      photo: "",
    };
  },
  mounted() {
    let temp = this.name.split(" ");
    this.photo = `https://nba-players.herokuapp.com/players/${temp[1]}/${temp[0]}`;
  },
};
</script>

<style>
.name {
  display: flex;
}
.team {
  display: flex;
}
</style>