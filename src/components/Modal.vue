<template>
    <div>
        <div class="shadow"></div>
        <section class="modal">
            <h2>{{ title }}</h2>
            <p>{{ message }}</p>
            <button @click="close">Close</button>
        </section>
    </div>
</template>

<script>
export default {
    props: [
        'title',
        'message'
    ],
    methods: {
        close() {
            this.$emit('closed');
        }
    }
}
</script>

<style lang="scss" scoped>
  @import "./styles/modal.scss";
</style>
