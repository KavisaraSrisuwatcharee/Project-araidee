<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-text-field v-model="name" label="First name" required></v-text-field>
      </v-col>

      <v-col cols="4">
        <v-text-field v-model="lastname" label="Last name" required></v-text-field>
      </v-col>

      <v-col cols="2">
        <v-text-field v-model="score" label="score" required></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-btn color="success" @click="addInfo()">ADD</v-btn>
      </v-col>
    </v-row>
    <v-data-table :headers="headers" :items="info" class="elevation-1"></v-data-table>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      name: "",
      lastname: "",
      score: "0",
      info: [],
      headers: [
        {
          text: "Name",
          value: "name",
        },
        {
          text: "LastName",
          value: "lastname",
        },
        {
          text: "Score",
          value: "score",
        },
      ],
    };
  },
  mounted() {
    axios.get("/data.json").then((response) => {
      this.info = response.data.data;
      this.info.sort(this.compare);
      this.info.reverse();
      console.log(response.data.data);
    });
  },
  methods: {
    addInfo() {
      let temp = {
        name: this.name,
        lastname: this.lastname,
        score: this.score,
      };
     let newdata=[...this.info,temp]
      newdata.sort(this.compare);
      newdata.reverse();
      this.info=newdata
      this.name = "";
      this.lastname = "";
      this.score = "0";
    },
    compare(a, b) {
      if (a.score < b.score) {
        return -1;
      } else if (a.score > b.score) {
        return 1;
      } else {
        return 0;
      }
    },
  },
};
</script>

<style>
</style>