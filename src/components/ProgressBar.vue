<template>
    <b-progress :value="value" :max="max" class="mb-3"></b-progress>

    
</template>

<script>
import { BProgress } from 'bootstrap-vue'
export default {
	components: { BProgress },

    data() {
      return {
        value: 33.333333333,
        max: 50
      }
    }

}
</script>

<style scoped>


</style>