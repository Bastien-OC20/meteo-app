<template>
  <div class="bloc-logo-info">
    <div class="bloc-logo">
      <img
        src="../assets/ressources/jour/04d.svg"
        alt="logo du temps qu'il fait"
        class="logo-meteo"
      />
    </div>

    <div class="bloc-info">
      <p class="temps"></p>
      <p class="temperature"></p>
      <p class="localisation"></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrentDay",
  props: {},
  data() {
    return {};
  },

  mounted() {},
};
</script>

<style>
.bloc-logo-info {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin: 0.1%;
}
.bloc-logo {
  width: 50%;
}
.bloc-logo img {
  width: 100%;
  height: auto;
}
.bloc-info {
  width: 50%;
}
.bloc-info .temps {
  font-size: 40px;
}
.bloc-info .temps::first-letter {
  text-transform: capitalize;
}
.bloc-info .temperature {
  font-size: 60px;
}
.bloc-info .localisation {
  font-size: 40px;
  word-wrap: break-word;
}
</style>
