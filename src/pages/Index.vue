<template>
  <q-page class="flex column">
    <div class="column" style="height: 100%">
    <div class="col q-pt-lg q-px-md">
        <q-input
          v-model="text"
          filled
          type="textarea"
          rows="19"
          dark
          @click="getWord"
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
        v-model="definition"
        type="textarea"
        rows="19"
        filled
        readonly
        dark
      />
    </div>
    </div>
  </q-page>

</template>

<script>
import { copyToClipboard } from 'quasar';
export default {
  name: 'PageIndex',
  data() {
    return {
      text: '',
      definition: ''
    }
  },
  methods: {
    copy(){
      console.log("Pressed the copy button.")
      copyToClipboard(this.text)
        .then(() => {
          // Success! Optionally, show a notification or toast
          console.log("Copied successfully.")
        })
        .catch(() => {
          // Failed to copy. Handle the error.
          console.log("Failed to copy.")
        });
    },
    getWord(event) {
      // Create a range object from the cursor position.
      const range = document.caretPositionFromPoint(event.clientX, event.clientY);

      if (range) {
        const textNode = range.offsetNode;
        const offset = range.offset;

        // Ensure we clicked inside a textarea.
        if (textNode.nodeType === Node.ELEMENT_NODE && textNode.tagName === 'TEXTAREA') {
          const text = textNode.value;
          
          // Find the start of the word.
          let start = offset;
          while (start > 0 && /\S/.test(text[start - 1])) {
            start--;
          }
          
          // Find the end of the word.
          let end = offset;
          while (end < text.length && /\S/.test(text[end])) {
            end++;
          }
          
          // Extract the word and update the component data.
          this.wordAtCursor = text.substring(start, end);
          this.definition = this.wordAtCursor;
        }
      }
    }
  }
}
</script>

<style lang="sass">
  .q-page
    background: linear-gradient(to bottom, #136a8a, #267871)
</style>