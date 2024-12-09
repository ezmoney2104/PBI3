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


-----

import { shallowMount } from '@vue/test-utils'
import HomeView from '@/components/HomeView.vue'
import CommonLabel from '@/components/common/CommonLabel.vue'
import { TITLELABEL } from '@/common/recipe/rCommonLabel'

describe('HomeView.vue', () => {
  let wrapper
  let mockDate

  beforeEach(() => {
    jest.useFakeTimers() // Mock setInterval
    mockDate = new Date('2024-12-09T12:34:56') // Fixed date for testing
    jest.setSystemTime(mockDate) // Mock the system time
    wrapper = shallowMount(HomeView, {
      stubs: {
        CommonLabel: true, // Stub CommonLabel component
      },
    })
  })

  afterEach(() => {
    jest.clearAllTimers()
    jest.useRealTimers()
  })

  it('should be a Vue instance', () => {
    expect(wrapper.exists()).toBe(true)
  })

  it('should render the correct number of app bar titles', () => {
    const labels = wrapper.findAll('.v-app-bar-title')
    expect(labels.length).toBe(TITLELABEL.length)
    labels.wrappers.forEach((labelWrapper, index) => {
      expect(labelWrapper.text()).toBe(TITLELABEL[index].display.label)
    })
  })

  it('should render the correct formatted date in the header', () => {
    const dateElement = wrapper.find('h4 span')
    expect(dateElement.text()).toBe(
      mockDate.toLocaleString('ja-JP', {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
        hour12: false,
      })
    )
  })

  it('should have the correct initial data', () => {
    expect(wrapper.vm.mainLabel).toEqual(TITLELABEL)
    expect(wrapper.vm.currentDate).toEqual(mockDate)
  })

  it('should update the currentDate every second', () => {
    const initialDate = wrapper.vm.currentDate
    jest.advanceTimersByTime(1000)
    expect(wrapper.vm.currentDate).not.toEqual(initialDate)
  })

  it('should format the current date correctly', () => {
    const formattedDate = wrapper.vm.formattedDate
    expect(formattedDate).toBe(
      mockDate.toLocaleString('ja-JP', {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
        hour12: false,
      })
    )
  })

  it('should clear the interval when component is unmounted', () => {
    const clearIntervalSpy = jest.spyOn(window, 'clearInterval')
    wrapper.unmount()
    expect(clearIntervalSpy).toHaveBeenCalledWith(wrapper.vm.interval)
  })
})

