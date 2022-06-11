<template>
  <div class="hello">
    <input v-model="animalName"
    type="text"  id="nameInput">
    <input v-model="imageURL" type="text"  id="imageInput">
    <button @click="postAnimal">POST</button>
    <button @click="getAnimals">GET</button>
  </div>

  
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      animalName: null,
      imageURL: null,
      animalArr:[]
    }
  },
  methods: {
    postAnimal() {

      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method: "POST",
        data : {
          animalName: this.animalName,
          imageURL: this.imageURL
        }
      }).then(()=>{
        this.getAnimals()
      }).catch((error)=>{
        console.log(error)
      })
    },
    getAnimals() {
      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method: "GET"
      }).then((response)=>{
        this.animalArr = response.data
        console.log(response.data)
      }).catch((error) =>{
        console.log(error)
      })
    }
 
  },
     mounted() {
      this.getAnimals()
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
