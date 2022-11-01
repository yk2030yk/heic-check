<template>
  <div class="hello">
    <h1>HEIC動作確認用</h1>

    <div class="border"></div>
    
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

    <div class="border"></div>

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

    <div class="border"></div>
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
h2 {
  color: rgb(48, 48, 169);
}
h3 {
  margin-top: 10px;
}
.hello {
  color: rgb(70, 70, 70);
  padding: 20px;
}
.border {
  background-color: rgb(173, 173, 173);
  height: 2px;
  width: 100%;
  margin: 30px 0
}
.result {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-left: auto;
  margin-right: auto;
  align-items: flex-start;
  background-color: rgb(249, 249, 249);
  border: solid 1px #ddd;
  padding: 10px;
  gap: 10px;
  margin-top: 10px;
}
.box {
  
}
</style>
