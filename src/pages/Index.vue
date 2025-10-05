<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
        <q-input
          v-model="text"
          filled
          type="textarea"
          rows="19"
          dark
        >
        </q-input>
    </div>
    <div class="col text-white align-middle text-right q-pt-md q-px-md">
      <q-btn 
        @click="copy"
        outline rounded color="white"
      >
        <span class="material-icons">
          content_copy
        </span>
        &nbsp;
        Copy
      </q-btn>
    </div>
    <div class="col text-center q-pt-lg q-px-md">
      <q-input
        v-model="myText"
        type="textarea"
        rows="19"
        filled
        readonly
        dark
      />
    </div>
  </q-page>

</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      text: '',
      myText: `This is a multiline text.
      The user can see this, but not edit it.`
    }
  },
  methods: {
    copy(){
      console.log("pressed the copy button")
    }
  }
}
</script>

<style lang="sass">
  .q-page
    background: linear-gradient(to bottom, #136a8a, #267871)
</style>