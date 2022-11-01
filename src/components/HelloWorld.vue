<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="file" @change="changeFile">
    <template v-if="file">
      <div>
        <h2>選択結果</h2>
        <div class="info">
          <div>size: {{ file.size }}</div>
          <div>name: {{ file.name }}</div>
          <div>mime: {{ file.mime }}</div>
        </div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => {
    return {
      file: undefined
    }
  },
  props: {
    msg: String
  },
  methods: {
    changeFile(e) {
      this.file = undefined

      const reader = new FileReader()
      const file = e.target.files[0]

      reader.readAsDataURL(file)
      reader.onload = () => {
        console.log(reader.result)

        const m = reader.result.match(/data:(.+);base64,/)

        this.file = {
          size: file.size,
          name: file.name,
          mime: m && m[1]
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
.info {
  display: flex;
  flex-direction: column;
  width: 500px;
  margin-left: auto;
  margin-right: auto;
  align-items: flex-start;
  background-color: #ddd;
  padding: 10px;
  gap: 10px;
  margin-top: 10px;
}
</style>
