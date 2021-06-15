<template>
    <input v-model="result"/>
</template>

<script lang="ts">
import { Prop, Vue } from 'vue-property-decorator';
export default class Screen extends Vue {
    @Prop() private result!:string; 
}

</script>
