<template>
  <!-- 71013943ccf9433c98d6babe4db0b13e -->


    <div class="sourceselection">
      <div class="jumbotron">
        <h2><span class="glyphicon glyphicon-list-alt"></span>News List</h2>
        <h4>Select News source</h4>
        <select class="form-control" v-on:change="sourceChanged">
          <option
            v-bind:value="source.id"
            v-for="source in sources"
            :key="source.id"
          >
            {{ source.name }}
          </option>
        </select>

        <div v-if="source">
          <h5 class="descrip">{{ source.description }}</h5>
          <a v-bind:href="source.url" class="btn btn-primary " target="_blank"
            ><h5>Go To {{ source.name }} Website</h5></a
          >
        </div>
      </div>
    </div>
  
</template>

<script>
// import { Link } from "vue-router";
export default {
  name: "source-selection",

  data() {
    return {
      sources: [],
      source: " ",
    };
  },

  methods: {
    sourceChanged: function (e) {
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id == e.target.value) {
          this.source = this.sources[i];
        }
      }
      console.log(e.target.value)
      this.$emit("sourceChanged", e.target.value);
    },
  },

  created: function () {
    this.$http
      .get("https://newsapi.org/v1/sources?language=en")
      .then((response) => {
        this.sources = response.data.sources;
      });
  },
};
</script>

<style   scoped>

*{
  margin-top: 20px;
}
.sourceselection{
    background-color: lightgrey;
    width: 100%;
    padding: 40px;
}

.descrip{
    padding-top: 10px;
}
</style>