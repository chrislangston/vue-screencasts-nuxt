<template>
  <span>
    <slot :minutes="minutes" :hours="hours">
      <span v-if="verbose">
        <span v-if="hours">{{hours}} hour{{hours > 1 ? 's' : ''}},</span>
        {{minutes}} minute{{minutes > 1 ? 's': ''}}
      </span>
      <span v-else>
        <span v-if="hours">{{hours}}:</span>{{ minutes }}:{{ seconds }}
      </span>
    </slot>
  </span>
</template>

<script>
  export default {
    computed: {
      hours(){
        return Math.floor(this.duration / 3600)
      },
      minutes(){
        let minutes = Math.floor((this.duration % 3600) / 60);
        
        let isSingleDigit = minutes.toString().length == 1
        if(isSingleDigit && this.useHours  && !this.verbose){
          minutes = `0${minutes}`
        }
        
        return minutes
      },
      seconds(){
        let seconds = this.duration % 60

        let isSingleDigit = seconds.toString().length == 1
        if(isSingleDigit && !this.verbose){
          seconds = `0${seconds}`
        }
        
        return seconds
      },
      useHours(){
        return this.duration > 60 * 60
      }
    },
    props: {
      duration: {
        type: [Number, String]
      },
      verbose: {
        type: Boolean,
        default: false
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>