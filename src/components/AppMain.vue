<template>
  <h1 v-if="sentence">
    {{ sentence}}
  </h1>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            wordArray: [],
            sentence: "",
            apiUrl: 'https://flynn.boolean.careers/exercises/api/random/word',
        }
    },
    methods: {
        generateWords() {
            for (let index = 0; index < 10; index++) {
                axios.get(this.apiUrl)
                    .then((response) => {
                      // handle success
                      console.log(response.data.response);
                      const results = response.data.response;
                      this.wordArray.push(results);
                      console.log(this.wordArray);
                      this.sentence = this.wordArray.join(' ');
                      console.log(this.sentence);
                    })
                    .catch((error) => {
                      // handle error
                      console.log(error);
                    })
                }
         }
    },
    created(){
       this.generateWords();
    },
   
}
</script>

<style>

</style>