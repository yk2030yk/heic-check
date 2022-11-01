<template>
  <div class="hello">
    <h1>HEIC動作確認用</h1>

    <div class="box">
      <h2>通常inputタグ</h2>
      <input type="file" @change="changeFile">
      <template v-if="file">
        <div>
          <h3>選択結果</h3>
          <div class="result">
            <div>size: {{ file.size }}</div>
            <div>name: {{ file.name }}</div>
            <div>mime: {{ file.mime }}</div>
          </div>
        </div>
      </template>
    </div>

    <div class="box">
      <h2>Vuetify v-file-input</h2>
      <v-file-input @change="changeVFile" />
      <template v-if="vfile">
        <div>
          <h3>選択結果</h3>
          <div class="result">
            <div>size: {{ vfile.size }}</div>
            <div>name: {{ vfile.name }}</div>
            <div>mime: {{ vfile.mime }}</div>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => {
    return {
      file: undefined,
      vfile: undefined
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
    },

    changeVFile(file) {
      this.vfile = undefined

      const reader = new FileReader()
      reader.readAsDataURL(file)
      reader.onload = () => {
        console.log(reader.result)

        const m = reader.result.match(/data:(.+);base64,/)

        this.vfile = {
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
  margin-top: 10px;
}
.hello {
  padding: 20px;
}
.result {
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
.box {
  margin-top: 30px;
}
</style>
