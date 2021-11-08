<template>
  <div class="jour-prevision-bloc">
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
    <div class="bloc-j">
      <p class="jour-prevision-nom"></p>
      <p class="jour-prevision-temp"></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "PrevisionDay",
  props: {},
  data() {
    return {};
  },

  mounted() {},
};
</script>

<style>
.jour-prevision-bloc {
    grid-area: 4 / 1 / 5 / -1;
}

.jour-prevision-bloc {
    display: grid;
    grid-template: 100px / repeat(7, 1fr);
}

.bloc-h, .bloc-j {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    border-top: 1px solid #f1f1f1;
    font-size: 21px;
}

.bloc-j:not(:last-child) {
    border-right: 1px solid #f1f1f1;
}

 .bloc-j p {
    margin: 5px;
}

</style>
