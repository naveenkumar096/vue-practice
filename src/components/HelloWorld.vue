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
            :style="{ width: monsterHealth + '%' }"
          >
            {{ monsterHealth }}
          </div>
        </div>
      </div>
    </section>
    <section class="row controls" v-show="!isStarted">
      <div class="small-12 columns">
        <button id="start-game" @click="startGame">START NEW GAME</button>
      </div>
    </section>
    <section class="row controls" v-show="isStarted">
      <div class="small-12 columns">
        <button id="attack" @click="attack">ATTACK</button>
        <button id="special-attack" @click="specialAttack">
          SPECIAL ATTACK
        </button>
        <button id="heal" @click="heal">HEAL</button>
        <button id="give-up" @click="giveUp">GIVE UP</button>
      </div>
    </section>
    <section class="row log">
      <div class="small-12 columns">
        <ul>
          <li v-for="(turn, index) in turns" :key="index">{{ turn.text }}</li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      userHealth: 100,
      monsterHealth: 100,
      isStarted: false,
      turns: []
    };
  },
  methods: {
    giveUp() {
      this.isStarted = false;
    },
    startGame() {
      this.isStarted = true;
      this.userHealth = 100;
      this.monsterHealth = 100;
      this.turns = [];
    },
    heal() {
      if (this.userHealth <= 90) {
        this.userHealth += 10;
      } else {
        this.userHealth = 100;
      }
      this.monsterAttack();
    },
    attack() {
      const damageAmount = this.damage(10, 3);
      this.monsterHealth -= damageAmount;
      this.turns.unshift({
        isPlayer: true,
        text: "Player hits to monster Damage" + damageAmount
      });
      if (this.checkWin()) {
        return;
      }
      this.monsterAttack();
    },
    monsterAttack() {
      const damageAmount = this.damage(12, 5);
      this.userHealth -= damageAmount;
      this.turns.unshift({
        isPlayer: true,
        text: "Monster hits Player Damage" + damageAmount
      });
      this.checkWin();
    },
    damage(min, max) {
      return Math.max(Math.floor(Math.random() * max, min));
    },
    specialAttack() {
      this.monsterHealth -= this.damage(10, 20);
      if (this.checkWin()) {
        return;
      }
      this.monsterAttack();
    },
    checkWin() {
      if (this.monsterHealth <= 0) {
        if (confirm("You Win ! Start A New Game ?")) {
          this.startGame();
        } else {
          this.isStarted = false;
        }
        return true;
      }
      if (this.userHealth <= 0) {
        if (confirm("You Lost Game ! Start A New Game ?")) {
          this.startGame();
        } else {
          this.isStarted = false;
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
