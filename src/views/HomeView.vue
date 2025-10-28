<template>
  <main id="sample">
    <h1>TinyMCE 富文本编辑器</h1>
    <TinyMceEditor
      v-model="content"
      :height="500"
      placeholder="请输入内容..."
    />
    <div class="preview-section">
      <h2>预览效果：</h2>
      <div class="preview-content" v-html="content"></div>
    </div>
  </main>
</template>

<script>
import TinyMceEditor from '@/components/TinyMceEditor.vue'

export default {
  name: 'HomeView',
  components: {
    TinyMceEditor
  },
  data() {
    return {
      content: '<p>Hello, world!</p>',
    }
  }
}
</script>

<style scoped lang="less">
#sample {
  display: flex;
  flex-direction: column;
  place-items: center;
  padding: 20px;
  
  h1 {
    margin-bottom: 30px;
    color: #2c3e50;
  }
}

.preview-section {
  margin-top: 40px;
  width: 100%;
  max-width: 1000px;
  
  h2 {
    margin-bottom: 20px;
    color: #42b983;
  }
  
  .preview-content {
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 20px;
    min-height: 100px;
    background: #f9f9f9;
    text-align: left;
  }
}

@media (min-width: 1024px) {
  #sample {
    width: 1000px;
  }
}
</style>