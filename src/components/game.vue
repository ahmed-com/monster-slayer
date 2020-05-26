<template>
    <div>
        <controls @attack="attack" @specialAttack="specialAttack" @heal="heal" @giveUp="giveUp"></controls>
        <result></result>
    </div>
</template>
<script>
import controls from './controls';
import result from './result';
import {eventBus} from '../main';

export default {
    data(){
        return {
            playerHealth : 100,
            monsterHealth : 100
        }
    },
    methods : {
        giveUp(){
            this.$emit('lose',this.monsterHealth)
            this.playerHealth = 100;
            this.monsterHealth = 100;
        },
        attack(){
            const playerDmg = Math.random() * 10;
            const monsterDmg = Math.random() * 10;
            this.playerHealth -= monsterDmg;
            this.monsterHealth -= playerDmg;
            eventBus.$emit('changePlayerHealth', -monsterDmg);
            eventBus.$emit('changeMonsterHealth', -playerDmg);
        },
        specialAttack(){
            const playerDmg = Math.random() * 30;
            const monsterDmg = Math.random() * 10;
            this.playerHealth -= monsterDmg;
            this.monsterHealth -= playerDmg;
            eventBus.$emit('changePlayerHealth', -monsterDmg);
            eventBus.$emit('changeMonsterHealth', -playerDmg);
        },
        heal(){
            let heal = Math.random()*10;
            let monsterDmg = Math.random() * 10;
            if((this.playerHealth + heal - monsterDmg) > 100){
                const diff = 100 - this.playerHealth;
                heal = (heal / (heal + monsterDmg)) * diff;
                monsterDmg = (monsterDmg / (heal + monsterDmg)) * diff;
            }
            this.playerHealth += (heal - monsterDmg);
            eventBus.$emit('changePlayerHealth', -monsterDmg);
            eventBus.$emit('changePlayerHealth',heal);
        }
    },
    components : {
        controls,
        result
    },
    watch : {
        playerHealth : function(health){
            if(health <= 0) this.$emit('lose',this.monsterHealth);
        },
        monsterHealth : function(health){
            if(health <= 0) this.$emit('win',this.playerHealth);
        }
    }
}
</script>
<style scoped>

</style>