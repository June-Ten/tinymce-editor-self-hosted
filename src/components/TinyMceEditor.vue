<template>
  <div class="tinymce-editor-wrapper">
    <div :id="editorId"></div>
  </div>
</template>

<script>

export default {
  name: 'TinyMceEditor',
  props: {
    value: {
      type: String,
      default: ''
    },
    height: {
      type: Number,
      default: 500
    },
    placeholder: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      editorId: this.generateUniqueId()
    }
  },
  mounted() {
    this.initEditor()
  },
  methods: {
    generateUniqueId() {
      // 生成唯一ID：时间戳 + 随机数
      const timestamp = Date.now()
      const random = Math.random().toString(36).slice(2, 9)
      return `tinymce-editor-${timestamp}-${random}`
    },
    initEditor() {
      const config = {
        selector: '#' + this.editorId,
        license_key: 'gpl',
        language: 'zh_CN',
        plugins: 'print preview searchreplace autolink directionality visualblocks visualchars fullscreen image link media template code codesample table charmap hr pagebreak nonbreaking anchor insertdatetime advlist lists wordcount textpattern noneditable help charmap quickbars emoticons',
        toolbar: 'undo redo | formatselect | bold italic underline strikethrough | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | blockquote | link image media table | charmap fullscreen preview | code',
        toolbar_mode: 'sliding',
        menubar: false,
        branding: false,
        statusbar: true,
      }
      tinymce.init(config)
    }
  }
}
</script>

<style scoped lang="less">
.tinymce-editor-wrapper {
  width: 100%;
  
  :deep(.tox-tinymce) {
    border: 1px solid #d9d9d9;
    border-radius: 4px;
    
    &:hover {
      border-color: #40a9ff;
    }
  }
  
  :deep(.tox-tinymce--focus) {
    border-color: #40a9ff;
    box-shadow: 0 0 0 2px rgba(24, 144, 255, 0.2);
  }
}
</style>
