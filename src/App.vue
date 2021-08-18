<template>
  <div id="app">
    <h2>Memory card game</h2>

    <cards-table />

    <form @submit.prevent="startGame">
      <button>Start new game</button>
    </form>

    <transition name="fade">
      <modal v-if="$store.state.modal" @closed="$store.commit('hideModal'); startGame();" :title="$store.state.modal.title" :message="$store.state.modal.message" />
    </transition>
  
  </div>
</template>

<script>
import CardsTable from './components/CardsTable.vue'
import Modal from './components/Modal.vue'

export default {
  data() {
    return {
      pairs: 8,
      color: 0
    }
  },
  created() {
    this.startGame();
    this.color = Math.floor(Math.random() * 360);
    this.updateColor();
    setInterval(() => {
      this.color ++;
      this.updateColor();
    }, 1000);
  },
  methods: {
    startGame() {
      if(this.pairs < 1 || this.pairs >= 200) {
        this.$store.commit('setModal', {
          title: "Wait... That's illegal",
          message: "You can't set that amount of card pairs"          
        });
        return;
      }
      this.$store.dispatch('startGame', parseInt(this.pairs));
    },
    updateColor() {
      document.documentElement.style.setProperty('--main-color', `hsl(${this.color}, 100%, 50%)`);
    }
  },
  components: {
    CardsTable,
    Modal
  }
}
</script>

<style lang="scss">
  @import "./app.scss";
</style>
