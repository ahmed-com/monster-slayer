<template>
    <section class="row controls">
        <div class="small-12 columns">
            <button id="start-game" @click="start">START NEW GAME</button>
        </div>
    </section>
</template>
<script>
export default {
    methods : {
        start(){
            this.$emit('start')
        }
    }
}
</script>
<style scoped>
    #start-game {
    background-color: #aaffb0;
  }

  #start-game:hover {
    background-color: #76ff7e;
  }
</style>