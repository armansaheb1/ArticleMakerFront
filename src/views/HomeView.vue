<template>
  <div style="padding: 5%; ">
      <div class="card">
        <div class="card-header">
          Article Maker
        </div>
      
        <div class="card-body">
          <label for="">Length</label>
          <select v-model="length" class="form-control" name="" id="">
            <option value="Short">Short</option>
            <option value="Medium Length">Medium</option>
            <option value="Long">Long</option>
          </select><br>
          <label for="">Tone</label>
          <select v-model="tone" class="form-control" name="" id="">
            <option value="Friendly">Friendly</option>
            <option value="Serious">Serious</option>
          </select><br>
          <label for="">Prompt</label>
          <textarea v-model="prompt" rows="8" class="form-control" name="" id="">
            
          </textarea><br>

          <button @click="send()" class="btn btn-dark form-control">Submit</button>
        </div>
    </div><br><br>

    <div v-if="result" class="card">
      <div class="card-body" style="padding:5%;text-align: justify;" v-html="result">
      </div>
    </div>

  </div>
 
  
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  data(){
    return {
      tone: 'Friendly',
      length: 'Short',
      prompt: '',
      result: ''
    }
  },
  methods:{
    async send(){
      await axios
      .post('articles', {prompt: this.prompt, length:this.length, tone: this.tone})
      .then(response => response.data)
      .then(response=>{
        this.result = response
      })
    }
  }
}
</script>
