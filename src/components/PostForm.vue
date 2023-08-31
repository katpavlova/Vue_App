<script>
import CustomInput from "@/components/UI/CustomInput.vue";
import CustomButton from "@/components/UI/CustomButton.vue";

  export default {
    components: {CustomInput, CustomButton},
    data(){
      return {
        newPost: {
          title: "",
          body: ""
        },
      }
    },
    methods: {
      createPost(){
        if(!this.newPost.title || !this.newPost.body) {
          return
        }
        this.$emit("create", this.newPost);
        this.newPost = {
          title: "",
          body: ""
        }
      }
    }
  }
</script>

<template>
  <form @submit.prevent>
    <div class="col-lg-4 col-12">
      <custom-input placeholder="Название" class="" v-model="newPost.title"/>
    </div>
    <div class="col-lg-4 col-12">
      <custom-input placeholder="Название" class="" v-model="newPost.body"/>
    </div>
    <div class="col-lg-4 col-12">
      <custom-button class="" @click="createPost">Добавить новую статью</custom-button>
    </div>



  </form>
</template>

<style scoped>

</style>