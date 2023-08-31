<script>
  export default {
    name: 'post-list',
    props: {
      posts: {
        type: Array,
        required: true
      }
    }
  }
</script>

<template>
  <div class="row mt-3">
    <div class="col-lg-4 col-12" v-for="post in posts" :key="post.id">
      <div class="postList__item mb-3">
        <h4>{{ post.title }}</h4>
        <p>{{ post.body }}</p>
      </div>

    </div>
  </div>
</template>

<style scoped>
.postList__item{
  border-radius: 10px;
  background: #FFF;
  min-height: 222px;
  padding: 20px 14px;
}

.postList__item h4{
  color: #000;
  font-size: 21px;
  font-style: normal;
  font-weight: 500;
  line-height: 150%;
}

.postList__item p{
  color: #555;
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 150%;
}
</style>