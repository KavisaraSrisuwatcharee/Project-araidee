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
    <v-row style="display:flex;justify-content:flex-end;padding:2%"><v-btn @click="save()">SAVE</v-btn></v-row>
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
      score: 0,
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
    });
  },
  methods: {
    addInfo() {
      let temp = {
        name: this.name,
        lastname: this.lastname,
        score: parseInt(this.score),
      };
      this.info.push(temp);
      this.info.sort(this.compare)
      this.name = "";
      this.lastname = "";
      this.score = 0;
    },
    save(){
      const blob = new Blob([JSON.stringify({data:this.info})], {type: 'text/plain'})
      const e = document.createEvent('MouseEvents'),
      a = document.createElement('a');
      a.download = "data.json";
      a.href = window.URL.createObjectURL(blob);
      a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
      console.log(a)
      e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
      a.dispatchEvent(e);
    },
    compare(a, b) {
      if (a.score < b.score) {
        return 1;
      } else if (a.score > b.score) {
        return -1;
      } else {
        return 0;
      }
    },
  },
};
</script>

<style>
</style>