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
      editorId: this.generateUniqueId(),
      editorInstance: null
    }
  },
  watch: {
    value(newVal) {
      if (this.editorInstance && this.editorInstance.getContent() !== newVal) {
        this.editorInstance.setContent(newVal || '')
      }
    }
  },
  mounted() {
    this.initEditor()
  },
  beforeDestroy() {
    this.destroyEditor()
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
        skin: 'oxide',
        content_css: 'default',
        height: this.height,
        placeholder: this.placeholder,
        plugins: 'preview searchreplace autolink directionality visualblocks visualchars fullscreen image link media code codesample table charmap pagebreak nonbreaking anchor insertdatetime advlist lists wordcount help charmap quickbars emoticons',
        toolbar: 'undo redo | formatselect | bold italic underline strikethrough | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | blockquote | link image media table | charmap fullscreen preview | code',
        toolbar_mode: 'sliding',
        menubar: false,
        branding: false,
        statusbar: true,
        resize: true,
        elementpath: true,
        quickbars_selection_toolbar: 'bold italic underline | link blockquote quickimage quicktable',
        quickbars_insert_toolbar: 'quickimage quicktable',
        contextmenu: 'link image table',
        automatic_uploads: true,
        file_picker_types: 'image',
        paste_data_images: true,
        images_upload_handler: async (blobInfo, progress) => {
          return new Promise((resolve, reject) => {
            const reader = new FileReader()
            reader.onload = () => {
              resolve(reader.result)
            }
            reader.onerror = () => {
              reject('图片读取失败')
            }
            reader.readAsDataURL(blobInfo.blob())
          })
        },
        setup: (editor) => {
          this.editorInstance = editor
          
          // 监听内容变化，实现双向绑定
          editor.on('input change keyup', () => {
            const content = editor.getContent()
            if (content !== this.value) {
              this.$emit('input', content)
            }
          })
        },
        init_instance_callback: (editor) => {
          console.log('初始化后', this.value)
          if (this.value) {
            editor.setContent(this.value)
          }
        }
      }
      
      tinymce.init(config).then(() => {
        this.editorInstance = tinymce.get(this.editorId)
      })
    },
    destroyEditor() {
      if (this.editorInstance) {
        this.editorInstance.destroy()
        this.editorInstance = null
      }
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
