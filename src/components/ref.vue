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
                <p> {{preview}} </p>
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
            color: 'background',    // dynamic class
            preview: ''
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
            console.log(this.$refs.input.autocapitalize="true") // it not supported for <input> element with a type attribute whose value is url, email, or password
            
            if(check == true)
            {
                this.$refs.input.style.background = 'yellow'
                this.preview = "email is valid" 
                console.log("email is valid")
            }
            else {
                this.$refs.input.style.background = 'red'
                this.preview = "email is invalid"
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