<template>
  <div>
    <button @click="changeTarget">change</button>
    <teleport :to="target">
      <span>teleport</span>
    </teleport>
  </div>
</template>

<script>
function* toggleTarget() {
  while (true) {
    yield document.querySelector("footer");
    yield "#teleport-container";
    yield document.querySelector("main");
  }
}
const toggle = toggleTarget();
export default {
  data() {
    return {
      target: "#teleport-container",
    };
  },
  methods: {
    changeTarget() {
      this.target = toggle.next().value;
    },
  },
};
</script>

<style scoped>
span {
  padding: 5px;
  margin:5px;
  background-color: rgba(70, 117, 148, 0.63);
  border-radius: .3rem;
}
</style>
