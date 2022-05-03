<template>
  <v-card>
    <v-container>
      <v-row>
        <v-text-field v-model="title" label="Title"></v-text-field>
        <v-text-field v-model="publishDate" label="Publish date"></v-text-field>
      </v-row>
    </v-container>
    <v-btn @click="onSearch" block> Search </v-btn>
    <v-col>
      <v-table fixed-header :search="title">
        <thead>
          <tr>
            <th class="text-left">Title</th>
            <th class="text-left">Description</th>
            <th class="text-left">Publish date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in booksList" :key="item.id">
            <td>{{ item.title }}</td>
            <td>{{ item.description }}</td>
            <td>{{ formatDate(item) }}</td>
          </tr>
        </tbody>
      </v-table>
    </v-col>
  </v-card>
</template>

<script lang='ts'>
import { defineComponent } from "vue";
import moment from "moment";

const SearchEvent = "onSearch";

export default defineComponent({
  name: "Datatable",
  data() {
    return {
      title: "",
      publishDate: "",
      booksList: [],
    };
  },
  props: {
    books: Array,
  },
  methods: {
    onSearch() {
      this.$emit(SearchEvent);
    },
    formatDate(item) {
      return moment(item.publishDate).format("MM/DD/YYYY hh:mm");
    },
    filter() {
      if (this.books.length > 0) {
        this.booksList = this.books.filter((book) => {
          let includesTitle = true;
          let includesDate = true;

          if (this.title != "" && this.title != null) {
            includesTitle = book.title.includes(this.title);
          }

          if (this.publishDate != "" && this.publishDate != null) {
            includesDate = book.publishDate.includes(this.publishDate);
          }

          return includesTitle && includesDate;
        });
      }
    },
  },
  watch: {
    books(newBooks) {
      this.booksList = newBooks;
    },
    title() {
      this.filter();
    },
    publishDate() {
      this.filter();
    },
  },
});
</script>