<template>
    <div>
        <div>
        <!-- <img alt="background gray" src="../assets/download.jpeg" width="100%"> -->
        <label> Email </label>
        <input :class="color" type="text" v-model.trim="data" ref="input">
        <button @click="checkEmail"> OK </button>
        </div>

            <div>
                <h1> PREVIEW </h1>
                <p> </p>
            </div>
    </div>
</template>

<script>
/* eslint-disable */
// import HelloWorld from '@/components/HelloWorld.vue'
export default {
    data () {
        return {
            data: '',
            color: 'background'                 // dynamic class
        }
    },
    components: {
        // 'hello-world': HelloWorld
    },
    methods: {
        checkEmail(){
            console.log(this.$refs.input.value)
            let reg = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/
            let check = reg.test(this.$refs.input.value)
            console.log(reg.test(this.$refs.input.value))
            console.log(this.$refs.input)
            console.log(this.$refs)
            console.log(this.$refs.input.autocapitalize="true")
            
            if(check == true)
            {''
                return this.$refs.input.style.background = 'yellow' 
                console.log("email is valid")
            }
            else {
                return this.$refs.input.style.background = 'red'
                console.log("email is invalid")
            }
        }
    }
    
}
</script>

<style scoped>
.background{
    font-size: 25px
}
</style>