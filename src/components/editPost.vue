<template>
  <div>
    <div>
      <!-- <img alt="background gray" src="../assets/download.jpeg" width="100%"> -->
      <div class="container">
        <center>
          <h1>
            <b>Edit Posts</b>
          </h1>
          <label>Title :</label>
          <input v-model="title" />
          <br />
          <label>Body:</label>
          <input v-model="body" />
          <br />
          <button class="btn btn-info" @click="editPost()">Edit Post</button>
        </center>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const url = "http://192.168.2.65:3030/posts/";
export default {
  props: ["post", "postId", "EditPost"],
  data() {
    return {
      id: 1,
      title: this.title,
      body: this.body
    };
  },
  methods: {
    editPost() {
      axios
        .patch(url + this.postId, { title: this.title, body: this.body })
        .then(response => (this.post = response.data.data));
      this.$emit("geteditData", this.EditPost);
    }
  }
};
</script>

<style scoped>
.container {
  /* margin-left:45% */
  margin-top: 12%;
}
input {
  border-radius: 4px%;
  padding: 5px 12px;
  width: 20%;
  padding: 0.6%;
  margin-left: 3%;
  margin-top: 3%;
  width: 50%;
  font-size: 25px;
}
label {
  /* padding-right: 2%; */
  font-weight: bold;
  font-size: 20px;
  padding-right: 2%;
}
.btn-info {
  margin-top: 3%;
  width: 10%;
}
</style>