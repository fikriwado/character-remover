<template>
  <v-container class="py-16">
    <v-row justify="center" class="pb-5">
      <v-col cols="12">
        <div class="text-h2 text-center">Character Remover</div>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" sm="5">
        <v-text-field label="Characters" v-model="characters"></v-text-field>
        <v-textarea label="Text" rows="8" v-model="text" hide-details></v-textarea>
        <v-row>
          <v-col cols="6">
            <v-checkbox v-model="removeFirstLineSpace" color="info" label="Remove first line space" hide-details></v-checkbox>
          </v-col>
          <v-col cols="6">
            <v-checkbox v-model="trimText" color="info" label="Trim text" hide-details></v-checkbox>
          </v-col>
        </v-row>
        <div class="text-caption pa-2 bg-grey-lighten-4">
          <div class="text-grey">NOTE</div>
          <div class="font-weight-medium">Add all characters you want to remove. Default: ",[]</div>
        </div>
      </v-col>
      <v-col cols="12" sm="5">
        <v-textarea label="Results" rows="15" v-model="results" readonly></v-textarea>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      characters: '",[]',
      text: '',
      removeFirstLineSpace: true,
      trimText: true
    }
  },
  computed: {
    getCharacters() {
      return this.characters.split('')
    },
    results() {
      let newText = this.getCharacters.reduce((acc, char) => {
        return acc.replaceAll(char, '')
      }, this.text)

      if (this.removeFirstLineSpace) newText = newText.replace(/^\s*/gm, '')
      if (this.trimText) newText = newText.trim()

      return newText
    }
  }
}
</script>
