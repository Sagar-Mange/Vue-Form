<template>
  <div>
    <!-- <ref></ref> -->
    <!-- <demo></demo> -->
    <div style="margin-top:8%;margin-bottom:8%" id="trainee-table">
      <div v-if="!addPost && !EditPost">
        <div class="container">
          <div class="table-wrapper">
            <div class="table-title">
              <div class="row">
                <div class="col-sm-4">

                    <!-- <i  class="material-icons glyphicon glyphicon-search"></i> -->
                    
                  <input
                    @keyup.enter="filterPosts"
                    placeholder="Enter Title Here"
                    type="text"
                    v-model="SearchString"
                    style="color:black"
                  />
              
                </div>

                <div class="col-sm-2">
                  <h2>
                    <b>POSTS</b>
                  </h2>
                </div>
                <div class="col-sm-6">
                  <button class="btn btn-success" @click="(addPost='true')">
                    <i class="material-icons">&#xE147;</i>
                    <span>Add Post</span>
                  </button>
                  <button class="btn btn-info" @click="getPost()">
                    <i class="material-icons glyphicon glyphicon-refresh"></i>
                  </button>
                </div>
              </div>
            </div>
            <table class="table table-striped table-hover">
              <thead>
                <tr>
                  <th>User Id</th>
                  <th>Title</th>
                  <th>Body</th>
                  <th>Actions</th>
                </tr>
              </thead>
              <tbody>
                <!-- <tr v-for="post in searchPost" :key="post"> -->
                <!-- <td> {{post.userId}} </td> -->

                <tr v-for="(post,index) in posts" :key="index">
                  <!-- <td v-for="(post,index) in filterPosts" :key="index"></td> -->

                  <td>{{ post.userId}}</td>
                  <!-- {{SearchString}} -->

                  <td>{{ post.title }}</td>
                  <!-- <td v-else>{{ post.title}}</td> -->

                  <td>{{ post.body }}</td>
                  <!-- <td v-else>{{ post.body}}</td> -->

                  <td>
                    <a href="#" @click="editPost(index,post._id)" class="edit" data-toggle="modal">
                      <i class="material-icons" data-toggle="tooltip" title="Edit">&#xE254;</i>
                    </a>
                    <a
                      href="#"
                      @click="deletePost(index,post._id)"
                      class="delete"
                      data-toggle="modal"
                    >
                      <i class="material-icons" data-toggle="tooltip" title="Delete">&#xE872;</i>
                    </a>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <div v-else>
        <addPost
          v-show="addPost"
          :post="post"
          :addPost="addPost"
          :postId="postId"
          @getData="getData($event)"
        />
        <editPost
          v-show="EditPost"
          :post="post"
          :Editpost="EditPost"
          :postId="postId"
          @geteditData="geteditData($event)"
        />
      </div>
    </div>
  </div>
</template>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>

<script>
/* eslint-disable */
import axios from "axios";
import addPost from "@/components/addPost.vue";
import editPost from "@/components/editPost.vue";
import ref from "@/components/ref.vue";
import demo from "@/components/demo.vue";

const API_URL = "http://192.168.2.65:3030/posts/";
export default {
  name: "trainee-table",
  components: {
    addPost: addPost,
    editPost: editPost,
    ref: ref,
    demo: demo
  },
  data() {
    return {
      posts: [],
      result: null,
      addPost: false,
      EditPost: false,
      postId: "",
      SearchString: this.SearchString
    };
  },

  created() {
    axios.get(API_URL).then(response => {
      this.posts = response.data.data;
      //   console.log(response.data.data);
    });
  },

  methods: {
    filterPosts() {
      this.posts = this.posts.filter(post => {
        if (post.title.match(this.SearchString)) {
          //   console.log("inside", post);
          return post;
        }
      });
    },

    getPost() {
      axios.get(API_URL).then(response => {
        response.data.data;
        this.posts = response.data.data;
      });
    },

    getData() {
      this.addPost = false;
    },

    geteditData() {
      this.EditPost = false;
    },

    deletePost(index, key) {
      axios.delete(API_URL + key).then(responce => {
        this.posts.splice(index, 1);
      });
    },
    editPost(index, key) {
      this.postId = key;
      this.EditPost = true;
    }
  }
};
</script>

<style scoped>
#app {
  color: #566787;
  font-family: "Varela Round", sans-serif;
  font-size: 13px;
}
.table-wrapper {
  background: #fff;
  padding: 20px 25px;
  margin: 25px 0;
  border-radius: 3px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.table-title {
  padding-bottom: 15px;
  background: #435d7d;
  color: #fff;
  padding: 16px 30px;
  margin: -20px -25px 10px;
  border-radius: 3px 3px 0 0;
}
.table-title h2 {
  margin: 5px 0 0;
  font-size: 24px;
}
.table-title .btn-group {
  float: right;
}
.table-title .btn {
  color: #fff;
  float: right;
  font-size: 13px;
  border: none;
  min-width: 50px;
  border-radius: 2px;
  border: none;
  outline: none !important;
  margin-left: 10px;
}
.table-title .btn i {
  float: left;
  font-size: 21px;
  margin-right: 5px;
}
.table-title .btn span {
  float: left;
  margin-top: 2px;
}
table.table tr th,
table.table tr td {
  border-color: #e9e9e9;
  padding: 12px 15px;
  vertical-align: middle;
}
table.table tr th:first-child {
  width: 60px;
}
table.table tr th:last-child {
  width: 100px;
}
table.table-striped tbody tr:nth-of-type(odd) {
  background-color: #fcfcfc;
}
table.table-striped.table-hover tbody tr:hover {
  background: #f5f5f5;
}
table.table th i {
  font-size: 13px;
  margin: 0 5px;
  cursor: pointer;
}
table.table td:last-child i {
  opacity: 0.9;
  font-size: 22px;
  margin: 0 5px;
}
table.table td a {
  font-weight: bold;
  color: #566787;
  display: inline-block;
  text-decoration: none;
  outline: none !important;
}
table.table td a:hover {
  color: #2196f3;
}
table.table td a.edit {
  color: #ffc107;
}
table.table td a.delete {
  color: #f44336;
}
table.table td i {
  font-size: 19px;
}
table.table .avatar {
  border-radius: 50%;
  vertical-align: middle;
  margin-right: 10px;
}
b {
  margin-left: 90%;
}
th {
  font-size: 17px;
}
td {
  font-family: "Courier New";
  font-size: 18px;
}
/* .temp::after {
  content: "........"
} */
</style>