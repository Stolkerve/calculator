<template>
    <button 
        class="button" 
        @click="(e)=>{callBack(text)}"
    >
    {{this.text}}
    </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Button extends Vue {
    @Prop() private text!:string;
    @Prop() private color!:string;
    @Prop() private callBack!:any;


}
</script>

<style>
.button {
    flex-grow: 1;
    padding: 15px;
    padding-left: 20px;
    padding-right: 20px;
    border: 0px;
    font-family: serif;
    font-size: 24px;
    text-align: center;
    background-color: rgb(253, 102, 1);
    color: #000;
    opacity: 0.8;
    transition: 0.3s;
}

.button:hover {
    opacity: 1
}
</style>