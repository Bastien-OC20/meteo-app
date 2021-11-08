<template>
  <div class="heure-bloc-prevision">
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
    <div class="bloc-h">
      <p class="heure-nom-prevision"></p>
      <p class="heure-prevision-valeur"></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrentHours",
  props: {},
  data() {
    return {};
  },

  mounted() {},
};
</script>

<style>
.heure-bloc-prevision {
    grid-area: 3 / 1 / 4 / -1;
}

.heure-bloc-prevision {
    display: grid;
    grid-template: 100px / repeat(7, 1fr);
}

.bloc-h {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    border-top: 1px solid #f1f1f1;
    font-size: 21px;
}

.bloc-h:not(:last-child) {
    border-right: 1px solid #f1f1f1;
}

.bloc-h p{
    margin: 5px;
}


</style>
