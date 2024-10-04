<template>
  <b-form @submit.prevent="formAddHandling">
    <div class="my-3" v-for="(item, id) in items" :key="id">
      <component
        :is="item.componentName"
        :key="resetKaibiganId"
        :input="item"
        @formData="addFormData"
        @change="eventHandler"
      ></component>
    </div>
  </b-form>
</template>

<script>
import CommonDropdown from '@/components/common/CommonDropdown.vue'
import { DROPDOWNPROPERTIES } from '@/common/recipe/rDropdownRecipe'
import CommonTextInput from '@/components/common/CommonTextInput.vue'
import { TEXTINPUTPROPERTIES } from '@/common/recipe/rTextInputRecipe'
import { TEXTAREAPROPERTIES } from '@/common/recipe/rTextArea'
import CommonTextArea from '@/components/common/CommonTextArea.vue'
import { RADIOPROPERTIES } from '@/common/recipe/rRadioRecipe'
import CommonRadio from '@/components/common/CommonRadio.vue'
import { CHECKBOXPROPERTIES } from '@/common/recipe/rCheckboxRecipe'
import CommonCheckbox from '@/components/common/CommonCheckBox.vue'
import CommonButton from '@/components/common/CommonButton.vue'
import { BUTTONPROPERTIES } from '@/common/recipe/rButtonRecipe'

export default {
  name: 'RegistrationForm',
  components: {
    CommonTextInput,
    CommonDropdown,
    CommonTextArea,
    CommonRadio,
    CommonCheckbox,
    CommonButton
  },
  data() {
    return {
      items: [
        ...TEXTINPUTPROPERTIES,
        ...DROPDOWNPROPERTIES,
        ...RADIOPROPERTIES,
        ...CHECKBOXPROPERTIES,
        ...TEXTAREAPROPERTIES,
        ...BUTTONPROPERTIES
      ],
      formData: {
        nickname: '',
        fullname: '',
        age: 0,
        birthday: '',
        email: '',
        phonenumber: '',
        personality: '',
        gender: '',
        love: [],
        motto: ''
      },

      isError: false,
      resetKaibiganId: 0
    }
  },

  methods: {
    /**
     * Function to handle the submit button and break it once formAddHandling function is used
     * @param {object} action - used assign and get the action taken of case statement
     */

    eventHandler(action) {
      switch (action) {
        case 'Submit':
          this.formAddHandling()
          break
      }
    },

    /**
     * Function to assign value to key
     * @param {object} data - used to assign and get key and value variable
     */

    addFormData(data) {
      this.formData[data.key] = data.value
    },

    /**
     * Used to dislpay data to console log and check errors and resets the array
     */

    formAddHandling() {
      if (!this.checkValidity() && this.isError == false) {
        console.log('Data Added:', this.formData)
        alert('Form Submitted!')

        this.$emit('addKaibigan', this.formData)

        this.resetKaibigan()
      }
    },

    /**
     * Function to reset formData
     *
     */

    resetKaibigan() {
      this.formData = {
        nickname: '',
        fullname: '',
        age: 0,
        birthday: '',
        email: '',
        phonenumber: '',
        personality: '',
        gender: '',
        love: [],
        motto: ''
      }

      this.resetKaibiganId += 1
    },

    /**
     * Function to check validity of forms
     */

    checkValidity() {
      const namePattern = /^[A-Za-z\s]+$/

      if (
        this.formData.fullname.length > 45 ||
        this.formData.fullname.trim() === '' ||
        !namePattern.test(this.formData.fullname)
      ) {
        alert('Fullname must not be greater than 45 characters or should not be blank')
        this.formData.fullname = ''
        this.isError = true
        return
      }

      if (
        this.formData.nickname.length > 20 ||
        this.formData.nickname.trim() === '' ||
        !namePattern.test(this.formData.nickname)
      ) {
        alert('Nickname must not be greater than 20 characters or should not be blank')
        this.formData.nickname = ''
        this.isError = true
        return
      }

      const agePattern = /^[1-9][0-9]$|^(100)$/

      if (!agePattern.test(this.formData.age)) {
        alert('Invalid number, Must be above 10-100yrs Old')
        this.formData.age = 0
        this.isError = true
        return
      }

      if (this.formData.birthday === '') {
        alert('Enter a birthday')
        this.formData.birthday = ''
        this.isError = true
        return
      }

      const emailPatternTest = /^[a-z0-9._-]+@[a-z.-]+\.[a-zA-Z]{2,}$/

      if (!emailPatternTest.test(this.formData.email)) {
        alert('Invalid email format, incude @ and no special characters')
        this.formData.email = ''
        this.isError = true
        return
      }

      const numberPattern = /^(09|\+639)\d{9}$/

      if (!numberPattern.test(this.formData.phonenumber)) {
        alert('Invalid Phone Number Format. Ex: 09123456789')
        this.formData.phonenumber = ''
        this.isError = true
        return
      }

      if (this.formData.personality == '' || this.formData.personality == null) {
        alert('Select your personality')
        this.isError = true
        return
      }

      if (this.formData.gender == '' || this.formData.gender == null) {
        alert('Select your Gender')
        this.isError = true
        return
      }

      if (this.formData.love.length !== 3) {
        alert('Pick your top 3 love languages')
        this.formData.love = []
        this.isError = true
        return
      }

      if (this.formData.motto.trim() === '') {
        alert('Please enter your motto')
        this.formData.motto = ''
        this.isError = true
        return
      } else {
        this.isError = false
        return
      }
    }
  }
}
</script>

<style scoped></style>
