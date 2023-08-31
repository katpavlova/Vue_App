<script>
  import axios from "axios";
  import PostForm from "@/components/PostForm.vue";
  import PostList from "@/components/PostList.vue";

  export default {
    components: {PostList, PostForm},
    data(){
      return {
        posts: [],
        postsVisible: [],
        pageNumber: 1,
        postsOnPage: 6,
        postsLoading: false,
        countPages: 1
      }
    },
    methods: {
      async fetchGetPosts(){
        try {
          this.postsLoading = true
          const response = await axios.get(
              "https://jsonplaceholder.typicode.com/posts",
              { params: { _limit: 20 } },
          );
          this.posts = response.data;
        } catch (err) {
          alert("Произошла ошибка при получении данных")
        } finally {
          this.postsLoading = false
        }
      },
      async createPost(newPost){
        try {
          const response = await axios.post(
              "https://jsonplaceholder.typicode.com/posts",
              {
                title: newPost.title,
                body: newPost.body,
                userId: 1,
              }
          );
          this.posts.unshift(response.data);

        } catch (err) {
          alert("Произошла ошибка при добавлении нового поста")
        }
      },
      changePage(pageNum){
        this.pageNumber = pageNum;
        this.postsVisible = this.identPostsVisible()
      },
      identPostsVisible(){
        return this.posts.slice(((this.pageNumber - 1) * this.postsOnPage), this.pageNumber * this.postsOnPage);
      }
    },
    mounted() {
      this.fetchGetPosts();
    },
    watch: {
      posts: {
        handler(){
          this.countPages = Math.ceil(this.posts.length / this.postsOnPage);
          this.postsVisible = this.identPostsVisible()

        },
        deep: true
      },
    }
  }
</script>

<template>
  <div class="app">
    <div class="container">
      <div class="row">
        <div class="logo col-12">
          <img src="./assets/logo.png" alt="">
        </div>
      </div>
      <post-form
          class="row mt-5"
          @create="createPost"
      />
      <div class="mt-5">
        <h2 class="col-12">Статьи</h2>
        <div v-if="postsLoading">
          <h2>Данные загружаются...</h2>
        </div>
        <div v-else>
          <post-list
              :posts="this.postsVisible"
          />
        </div>
      </div>
      <div v-if="!postsLoading" class="row mt-4">
        <div class="navigation">
          <button
            v-for="pageNum in countPages"
            class="navigation__btn"
            :class="{navigation__btn_active: pageNumber === pageNum}"
            :key="pageNum"
            @click="changePage(pageNum)"
          >
            {{ pageNum }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.app{
  background-image: url("./assets/bg.png");
  background-repeat: no-repeat;
  background-size: cover;

  min-height: 100vh;
  padding-top: 80px;
  padding-bottom: 90px;
}

h2{
  color: white;
}

.navigation__btn {
  border: none;
  width: 30px;
  height: 35px;
  border-radius: 5px;
  background: #B0B4FF;
  margin-right: 10px;
}

.navigation__btn_active{
  background: #fff;
  font-weight: bold;
}
</style>