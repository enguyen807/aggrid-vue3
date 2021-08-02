<template>
  <div class="h-100">
    <!--begin::Switch-->
    <label
      id="action-switch-label"
      class="
        form-check
        form-switch
        form-check-custom
        form-check-solid
        form-check-label
        h-100
      "
    >
      <!--begin::Input-->
      <input
        id="action-switch-input"
        class="form-check-input"
        name="switch-action"
        type="checkbox"
        @click="handleCheckbox"
        :value="getValue"
        :checked="switchValue > 0 ? true : false"
      />
      <!--end::Input-->
    </label>
    <!--end::Switch-->
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "AgGridActions",
  props: ["values"],
  setup() {
    const switchValue = ref(0);

    const handleCheckbox = (e) => {
      if (e.target.checked) {
        switchValue.value = 1;
      } else {
        switchValue.value = 0;
      }
    };

    const getValue = () => {
      return switchValue.value;
    };

    return {
      handleCheckbox,
      getValue,
    };
  },
});
</script>

<style>
#action-switch-label {
  justify-content: center;
}
</style>