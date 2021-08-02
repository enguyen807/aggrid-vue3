<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
  <div>
    <ag-grid-vue
      style="width: 100%; height: 500px"
      class="ag-theme-alpine"
      :columnDefs="columnDefs"
      :rowData="rowData"
      :defaultColDef="defaultColDef"
      editType="fullRow"
      rowSelection="single"
      :frameworkComponents="frameworkComponents"
    >
    </ag-grid-vue>
  </div>
</template>

<script lang="ts">
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-alpine.css";
import { defineComponent, ref, reactive, onBeforeMount } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import { AgGridVue } from "ag-grid-vue3";
import AgGridSwitch from "@/components/BaseSwitch.vue";

export default defineComponent({
  name: "App",
  components: {
    // HelloWorld,
    AgGridVue,
  },
  setup() {
    const columnDefs = ref();
    const rowData = ref();
    const defaultColDef = ref();

    const frameworkComponents = reactive({
      AgGridSwitch,
    });

    onBeforeMount(() => {
      columnDefs.value = [
        { field: "make" },
        {
          field: "activate",
          cellEditorFramework: frameworkComponents.AgGridSwitch,
        },
        { field: "model" },
        { field: "price" },
      ];

      defaultColDef.value = {
        flex: 1,
        editable: true,
      };

      rowData.value = [
        { make: "Toyota", activate: 0, model: "Celica", price: 35000 },
        { make: "Ford", activate: 1, model: "Mondeo", price: 32000 },
        { make: "Porsche", activate: 0, model: "Boxter", price: 72000 },
      ];
    });

    return {
      columnDefs,
      defaultColDef,
      rowData,
      frameworkComponents,
    };
  },
});
</script>

<style>
#app {
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
