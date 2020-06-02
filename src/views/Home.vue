<template>
  <div class="home">
    <DataComponent msg="Tabla" :itemsDB="dataElements" />
  </div>
</template>

<script>
// @ is an alias to /src
import DataComponent from "@/components/DataComponent.vue";
import jsonFile from "./itemsDB.json";

export default {
  name: "Home",
  components: {
    DataComponent
  },
  data() {
    return {
      dataElements: jsonFile
    };
  }
};
</script>
