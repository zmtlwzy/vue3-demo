<template>
  <div class="column-layout">
    <h3>CustomRef</h3>
    <input v-model="text" />
    <span class="ma">{{ text }}</span>
  </div>
</template>

<script>
import { customRef } from "vue";
function useDebouncedRef(value, delay = 500) {
  let timeout;
  return customRef((track, trigger) => {
    return {
      get() {
        track();
        return value;
      },
      set(newValue) {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          value = newValue;
          trigger();
        }, delay);
      },
    };
  });
}

export default {
  name: "CustomRef",
  setup() {
    return {
      text: useDebouncedRef("hello"),
    };
  },
};
</script>

<style></style>
