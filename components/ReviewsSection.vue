<template>
  <div>
    <div class="title" id="reviews">
      <span class="titulo-text">Customer’s</span>
      <span class="subtitulo-text" :style="{ marginLeft: '1rem' }">Review</span>
    </div>
    <v-container grid-list-xl>
      <v-layout row wrap>
        <v-flex md6>
          <v-card v-for="(comment, index) in comments" :key="index">
            <v-card-title>
              <h2>{{ comment.name }}</h2>
            </v-card-title>
            <v-card-text>
              <p>{{ comment.review }}</p>
            </v-card-text>
            <v-btn @click="deleteComment(index)" color="error">Delete</v-btn>
          </v-card>
        </v-flex>
        <v-flex md6>
          <v-form @submit.prevent="addComment">
            <v-text-field v-model="newComment.name" label="Name" required></v-text-field>
            <v-textarea v-model="newComment.review" label="Review" required></v-textarea>
            <v-btn type="submit" color="primary">Add Review</v-btn>
          </v-form>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comments: [
        { name: "Carlos", review: "Deliciosas donas, las mejores que he probado." },
        { name: "Ana", review: "Excelente servicio y sabor incomparable." }
      ],
      newComment: {
        name: '',
        review: '',
      },
    };
  },
  methods: {
    addComment() {
      if (this.newComment.name && this.newComment.review) {
        this.comments.push({ ...this.newComment });
        this.newComment.name = '';
        this.newComment.review = '';
      }
    },
    deleteComment(index) {
      this.comments.splice(index, 1);
    },
  },
};
</script>

<style scoped src="@/assets/reviews-section.css"></style>
