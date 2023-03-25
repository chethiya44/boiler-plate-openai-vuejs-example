<template>
  <div>
     <h1>This is a boiler Plate of open ai Powered vue js Word Count reduce application</h1>
    <form method="post" @submit.prevent="submitText">
      <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Input Text</label>
          <textarea type="email" class="form-control" id="exampleInputEmail1" name="inputText"  v-model="userInputtext" aria-describedby="emailHelp"></textarea>
          <label for="exampleInputEmail1" class="form-label">Select Number of word Reduction you want</label>
          <div class="btn-group" style="margin-top: 10px">
                  <select class="form-select" aria-label="Default select example" name="value" v-model="userinputValue">
                      <option value="5">5</option>
                      <option value="10">10</option>
                      <option value="15">15</option>
                      <option value="10">10</option>
                  </select>
          </div>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
    {{outputText}}
    </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      userInputtext: '',
      userinputValue: '',
      outputText: '',
      apiKey: 'sk-xxxxxxxxxxxxxxxxxxxx', // Replace with your actual API key
      apiEndpoint: 'https://api.openai.com/v1/chat/completions' // Replace <YOUR_slected model> 
    }
  },
  methods: {
    async submitText() {
      const response = await axios.post(
        this.apiEndpoint,
        {
           model:'gpt-3.5-turbo',
            messages : 
               [{"role": "user", "content": 'Reduce this senentce words'+this.userInputtext+ 'into'+ this.userinputValue +'words sentance'}],
        },
        {
          headers: {
            Authorization: `Bearer ${this.apiKey}`,
            'Content-Type': 'application/json'
          }
        }
      )
      this.outputText = response.data.choices[0].message.content
    }
  }
}
</script>