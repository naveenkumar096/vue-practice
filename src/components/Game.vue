<template>
  <div id="app">
    <section class="row">
      <div class="small-6 columns">
        <h1 class="text-center">YOU</h1>
        <div class="healthbar">
          <div
            class="healthbar text-center"
            style="background-color: green; margin: 0; color: white;"
            :style="{ width: userHealth + '%' }"
          >
            {{ userHealth }}
          </div>
        </div>
      </div>
      <div class="small-6 columns">
        <h1 class="text-center">MONSTER</h1>
        <div class="healthbar">
          <div
            class="healthbar text-center"
            style="background-color: green; margin: 0; color: white;"
          ></div>
        </div>
      </div>
    </section>
    <section class="row controls" v-if="!isStarted">
      <div class="small-12 columns">
        <button id="start-game">START NEW GAME</button>
      </div>
    </section>
    <section class="row controls" v-else>
      <div class="small-12 columns">
        <button id="attack">ATTACK</button>
        <button id="special-attack">
          SPECIAL ATTACK
        </button>
        <button id="heal">HEAL</button>
        <button id="give-up">GIVE UP</button>
      </div>
    </section>
    <section class="row log">
      <div class="small-12 columns">
        <ul>
          <li></li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Game",
  data() {
    return {
      userHealth: 100,
      monsterHealth: 100,
      isStarted: false,
      turns: []
    };
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
