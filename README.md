# TinyMCE Vue 富文本编辑器

这是一个基于 Vue 2 和 TinyMCE 的富文本编辑器项目。

## 项目特性

- ✅ TinyMCE 富文本编辑器封装
- ✅ 中文界面支持
- ✅ 完整的工具栏和插件
- ✅ 图片上传功能
- ✅ 响应式设计
- ✅ 实时预览

## 安装依赖

```bash
npm install
```

## 开发运行

```bash
npm run serve
```

## 生产构建

```bash
npm run build
```

## 使用说明

### TinyMceEditor 组件

已封装好的 TinyMCE 编辑器组件位于 `src/components/TinyMceEditor.vue`

#### 基本用法

```vue
<template>
  <TinyMceEditor
    v-model="content"
    :apiKey="apiKey"
    :height="500"
    placeholder="请输入内容..."
  />
</template>

<script>
import TinyMceEditor from '@/components/TinyMceEditor.vue'

export default {
  components: {
    TinyMceEditor
  },
  data() {
    return {
      content: '',
      apiKey: 'your-api-key'
    }
  }
}
</script>
```

#### Props 参数

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| value | String | '' | 编辑器内容（v-model） |
| apiKey | String | 'no-api-key' | TinyMCE API 密钥 |
| height | Number | 500 | 编辑器高度 |
| placeholder | String | '' | 占位符文本 |

#### 功能特性

- 🔧 完整的富文本编辑功能
- 🌍 中文语言界面
- 🖼️ 图片上传和粘贴
- 📝 表格、链接、列表等常用功能
- 🎨 代码高亮和格式化
- 📱 响应式工具栏
- ⚡ 快速工具栏（选中文本时显示）

### 自定义配置

如需自定义编辑器的功能，请编辑 `src/components/TinyMceEditor.vue` 文件中的 `editorInit` 配置对象。

## 项目结构

```
my-project/
├── src/
│   ├── components/
│   │   └── TinyMceEditor.vue    # TinyMCE 封装组件
│   ├── views/
│   │   └── HomeView.vue         # 使用示例
│   ├── App.vue
│   └── main.js
└── package.json
```

## 技术栈

- Vue 2.6.14
- TinyMCE Vue 3.2.8
- Vue Router
- Vuex
- Less

## 配置参考

详见 [Vue CLI 配置参考](https://cli.vuejs.org/config/)
