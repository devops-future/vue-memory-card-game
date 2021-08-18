<template>
    <transition name="flip">
        <div v-if="!table[id].animating" class="card" @click="open">
            <span v-if="table[id].opened | table[id].found">{{ table[id].value }}</span>
        </div>
    </transition>
</template>

<script>
import { mapState } from 'vuex'

export default {
    methods: {
        open() {
            if(this.$store.state.table[this.id].found) return;
            this.$store.dispatch('openCard', this.id);
        }
    }, 
    props: {
        id: Number
    },
    computed: {
        ...mapState([
            'table'
        ])
    }
}
</script>

<style scoped lang="scss">
    @import "./styles/card.scss";
</style>
