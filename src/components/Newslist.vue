<template>
  
    <div class="newslist">
      <div class="container">
        <ol class="media-list">
          <li class="media" v-for="article in articles" :key="article.id">
            <div media-left>
              <a v-bind:href="article.url" target="_blank">
                <img
                  class="media-object"
                  v-bind:src="article.urlToImage"
                  alt=""
                />
              </a>
            </div>

            <div class="media-body">
              <h4 class="media-heading">
                <a v-bind:href="article.url" target="_blank">{{
                  article.title
                }}</a>
              </h4>
              <h5>
                <i>{{ article.author }}</i>
              </h5>
              <p>{{ article.description }}</p>
            </div>
          </li>
        </ol>
      </div>
    </div>
  
</template>

<script>
export default {
  name: "news-list",

  props: ["source"],

  data() {
    return {
      articles: [],
    };
  },

  methods: {
    updateSource: function (source) {
      console.log("Source", source);
      const getNews = async () => {
        try {
          const response = await this.$http.get(
            `https://newsapi.org/v1/articles?source=${source}&apiKey=d2a399c3d5b64e8c9903224c18362f82`
          );
          this.articles = response.data.articles;
        } catch (e) {
          console.log("Error occured", e);
        }
      };
      getNews();
    },
  },

  created: function () {
    this.updateSource(this.source || "abc-news-au");
  },

  watch: {
    source: function (val) {
      console.log("I was updated with -->", val);
      this.updateSource(val);
    },
  },
};
</script>

<style scoped>
.media-object {
  width: 450px;
  margin: 0 auto;
  padding: 30px;
}

.media {
  border-top: 2px solid lightgrey;
  padding-top: 40px;
      display: flex;

}


</style>