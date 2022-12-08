<template>
  <div class="category">
    <div class="container">
      <div class="row">
        <div class="col-12 text-center">
          <h3 class="pt-3">add category</h3>
        </div>
        <div class="row">
          <div class="col-3"></div>
          <div class="col-6">
            <form>
              <div class="form-group">
                <label>category name: </label>
                <input
                  type="text"
                  class="form-control"
                  v-model="categoryName"
                />
              </div>
              <div class="form-group">
                <label>category description: </label>
                <textarea
                  type="text"
                  class="form-control"
                  v-model="description"
                />
              </div>
              <div class="form-group">
                <label>category image: </label>
                <input type="text" class="form-control" v-model="imgUrl" />
              </div>
              <button
                type="button"
                class="btn btn-primary"
                @click="addCategory"
              >
                Done
              </button>
            </form>
          </div>
          <div class="col-3"></div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const axios = require("axios");
const sweetalert = require("sweetalert");
export default {
  data() {
    return {
      categoryName: "",
      description: "",
      imageUrl: "",
    };
  },
  methods: {
    addCategory() {
      console.log(this.categoryName, this.description);
      const newCategory = {
        categoryName: this.categoryName,
        description: this.description,
        imageUrl: this.imageUrl,
      };
      const baseURL = "https://limitless-lake-55070.herokuapp.com";
      axios({
        method: "post",
        url: `${baseURL}/category/create`,
        data: JSON.stringify(newCategory),
        headers: {
          "Content-Type": "application/json",
        },
      })
        .then(() => {
          sweetalert({
            text: "category added !",
            icon: "success",
          });
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
<style scoped>
</style>