<template>
  <v-layout>
    <v-app-bar color="#263238" dark>
      <v-app-bar-title v-for="label in mainLabel" :key="label.id" class="text-h6">
        {{ label.display.label }}
      </v-app-bar-title>
      <h4 class="mr-4 text-h6" style="color: #e3f2fd">
        <span>{{ formattedDate }}</span>
      </h4>
    </v-app-bar>
  </v-layout>
</template>

<script>
import CommonLabel from '../common/CommonLabel.vue'
import { TITLELABEL } from '@/common/recipe/rCommonLabel'
export default {
  name: 'HomeView',
  components: { CommonLabel },

  data() {
    return {
      mainLabel: TITLELABEL,
      currentDate: new Date(),
    }
  },

  /**
   * Mounted function to set the interval of the date to 1000 seconds
   */

  mounted() {
    this.interval = setInterval(() => {
      this.currentDate = new Date()
    }, 1000)
  },

  beforeUnmount() {
    clearInterval(this.interval)
  },

  computed: {
    /**
     * Function to return the formatted date YYYY/MM/DD HH: MM: SS
     */

    formattedDate() {
      return this.currentDate.toLocaleString('ja-JP', {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
        hour12: false,
      })
    },
  },
}
</script>
