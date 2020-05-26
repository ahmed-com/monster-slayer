<template>
    <section class="row">
        <div class="small-6 columns">
            <h1 class="text-center">YOU</h1>
            <div class="healthbar">
                <div class="healthbar text-center" style="background-color: green; margin: 0; color: white;" :style="playerHealthBar">

                </div>
            </div>
        </div>
        <div class="small-6 columns">
            <h1 class="text-center">MONSTER</h1>
            <div class="healthbar">
                <div class="healthbar text-center" style="background-color: green; margin: 0; color: white;" :style="monsterHealthBar">

                </div>
            </div>
        </div>
    </section>
</template>
<script>
import {eventBus} from '../main';

export default {
    data(){
        return {
            playerHealth : 100,
            monsterHealth : 100
        }
    },
    computed : {
        playerHealthBar(){
            const h = this.playerHealth;
            return {"width" : `${h}%`}
        },
        monsterHealthBar(){
            const h = this.monsterHealth;
            return {"width" : `${h}%`}
        }
    },
    created(){
        eventBus.$on('changePlayerHealth',dHealth =>{
            this.playerHealth += dHealth;
        });
        eventBus.$on('changeMonsterHealth',dHealth =>{
            this.monsterHealth += dHealth;
        });
        eventBus.$on('reset',_=>{
            this.playerHealth = 100;
            this.monsterHealth = 100;
        })
    }
}
</script>
<style scoped>
    .healthbar {
        width: 80%;
        height: 40px;
        background-color: #eee;
        margin: auto;
        transition: width 500ms;
    }
</style>