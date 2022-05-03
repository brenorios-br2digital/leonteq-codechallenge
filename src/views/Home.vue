

<template>
  <v-container>
    <Datatable :books="books" @onSearch="getBooks" />
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Datatable from "../components/Datatable.vue";

const BASEURL = "https://fakerestapi.azurewebsites.net";
const BOOKSENDPOINT = "/api/v1/Books";

export default defineComponent({
  name: "Home",
  data() {
    return {
      books: [],
    };
  },
  components: {
    Datatable,
  },
  methods: {
    async getBooks() {
      try {
        const res = await fetch(BASEURL + BOOKSENDPOINT);
        this.books = await res.json();
      } catch (err) {
        console.log(err);
      }
    },
  },
});
</script>