<script setup>
  import { ref } from 'vue'
  import axios from 'axios'
  let textDefault = ref('')
  let textTranslate = ref('')
  let disabled = ref(false)
  const translate = async () => {
    disabled.value = true
    try {
      const { data, status } = await axios.post(`http://10.192.3.36:9000/text`, {
        text: textDefault.value
      })
      if (status === 200) {
        textTranslate.value = data?.new_text
      }
    } catch (e) {
      console.log(e)
      alert('Nasazlyk yuze cykdy !')
    } finally {
      disabled.value = false
    }
  }
  const clear = () => {
    textDefault.value = ''
    textTranslate.value = ''
  }
</script>
<template>
  <v-container>
    <v-row class="text-center"
      ><v-col cols="12" md="6">
        <v-textarea name="input-7-1" label="Text" v-model="textDefault"></v-textarea> </v-col
      ><v-col cols="12" md="6">
        <v-textarea name="input-7-1" label="Text" v-model="textTranslate"></v-textarea>
      </v-col>
      <v-col cols="12" md="6">
        <v-btn
          color="primary"
          size="large"
          :disabled="disabled || textDefault === ''"
          @click="translate"
        >
          Translate
        </v-btn>
      </v-col>
      <v-col cols="12" md="6">
        <v-btn color="error" size="large" @click="clear">Clear</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>
