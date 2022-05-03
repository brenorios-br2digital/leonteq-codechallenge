<template>
  <v-card>
    <v-btn @click="onSearch" block> Search </v-btn>

    <v-col>
      <v-table fixed-header>
        <thead>
          <tr>
            <th class="text-left">Title</th>
            <th class="text-left">Description</th>
            <th class="text-left">Publish date</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in books" :key="item.id">
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
    return {};
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
  },
});
</script>