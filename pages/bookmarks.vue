<template>
  <v-container grid-list-md text-xs-center>
    <v-layout row wrap>
      <v-flex v-for="(book, index) in books" :key="index" xs3>
        <v-card class="text-xs-center">
          <v-flex xs6 offset-xs3>
            <v-img contain :src="book.imageUrl" height="250px" />
          </v-flex>
          <v-card-actions class="justify-center">
            <v-btn color="#70acb1" flat nuxt :to="`book/${book.id}`">
              View
            </v-btn>
            <!-- <v-btn color="#70acb1" flat nuxt :to="`login`">
              Bookmark
            </v-btn> -->
            <v-btn color="#70acb1" flat nuxt :to="`read/${book.id}`">
              Read
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
export default {
  // Access only if user is authenticated
  middleware: 'authenticated',
  data() {
    return {
      books: [],
      user: this.$auth.user
    }
  },
  async asyncData({ store, $axios }) {
    const data = await $axios.$get(
      `/content/user/bookstoread/${store.$auth.$state.user.id}`
    )
    console.log(data)
    return { books: data }
  }
}
</script>

<style scoped>
.card-title {
  color: #70acb1;
}
</style>
