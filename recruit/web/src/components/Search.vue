<template>
  <div>
    <input type="text" id="searchinp" placeholder="Enter quote or author to search" v-model="search" />
    <div class="panel panel-default">
          <div class="panel-heading">
            Existing Quotes
          </div>
        </div>
    <quote-list :quotes="filteredQuotes" />
  </div>
</template>
<script>
import QuoteList from "./QuoteList";
export default {
  data() {
    return {
      quotes: [],
      search: "",
    };
  },
  components: {QuoteList},
  mounted() {
    this.fetchQuotes();
  },
  computed: {
    filteredQuotes: function() {
      var self = this;
      return this.quotes.filter(function(val) {
        return (
          val.author.toLowerCase().indexOf(self.search.toLowerCase()) >= 0 ||
          val.text.toLowerCase().indexOf(self.search.toLowerCase()) >= 0
        );
      });
    }
  },
  methods: {
    fetchQuotes() {
      this.$feathers
        .service("quotes")
        .find()
        .then(result => {
          this.quotes = result.data;
        })
        .catch(() => {
          console.log("An error occurred while retreiving quotes.");
        });
    }
  }
};
</script>
<style scoped>
#searchinp{
    position: relative;
    left: 20%;
    bottom: 35px;
    border-radius: 5px;
    width: 50%;
    padding-left:10px;
}
</style>