<template>
    <section class="row log">
        <div class="small-12 columns">
            <ul>
                <li v-for="(message,index) in messages" :key="index">
                    {{message}}
                </li>
            </ul>
        </div>
    </section>
</template>
<script>
import {eventBus} from '../main';

export default {
    data(){
        return {
            messages : []
        }
    },
    created(){
        eventBus.$on('changePlayerHealth',difference=>{
            let message = `The monster attacked you with damage ${-difference}`;
            if(difference > 0) message = `you have healed up with  ${difference} HP`;
            this.messages.unshift(message);
        });
        eventBus.$on('changeMonsterHealth',difference=>{
            const message = `You have attacked the monster with damage ${-difference}`;
            this.messages.unshift(message);
        });
    }
}
</script>
<style scoped>

</style>