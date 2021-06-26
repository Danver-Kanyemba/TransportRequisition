<template>
  <div class="about">
    <h1>This is an about {{ user }}</h1>
  </div>
</template>

<script>
import axios from "axios";
axios.defaults.withCredentials = true;
axios.defaults.baseURL = "http://api.larawithsanctum.test/";

export default {
  data: ()=> ({
    user:[],
  }),
  mounted() {
    axios.get("/api/user").then((res) => {
      this.user = res.data.name;
      console.log(res);
    });
  },
};
</script>
