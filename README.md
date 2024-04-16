# lc-vue-select-input

选择器样式组件

常用场景：

- 配合 element-plus 中的 table 组件实现动态容器固定表头

## Demo

[demo](https://unpkg.com/lc-vue-select-input/docs/.vitepress/dist/index.html) 

## 安装 

```
npm i lc-vue-select-input 
```

## 例子

```vue
<template>
  <p>
    <select-input
      clearable
      @click='onClick'
      @clear-click='onClearClick'>
      <template #icon>
        <el-icon><circle-check /></el-icon>
      </template>
    </select-input>
  </p>
  <p>
    <select-input
      v-model='value'
      clearable
      @click='onClick'
      @clear-click='onClearClick' />
  </p>
  <p>
    <select-input
      v-model='value'
      @click='onClick'
      @clear-click='onClearClick' />
  </p>
  <p>
    <select-input
      v-model='value'
      clearable
      disabled
      @click='onClick'
      @clear-click='onClearClick' />
  </p>
  <p>
    <select-input
      :model-value='["a","b"]'
      multiple
      clearable
      disabled
      @click='onClick'
      @clear-click='onClearClick'>
      <template #icon>
        <el-icon><circle-check /></el-icon>
      </template>
    </select-input>
  </p>
  <p>
    <select-input
      :model-value='[]'
      clearable
      multiple
      @click='onClick'
      @clear-click='onClearClick'
      @multiple-tag-remove='onMultipleTagRemove' />
  </p>
  <p>
    <select-input
      :model-value='["a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b"]'
      multiple
      @click='onClick'
      @clear-click='onClearClick'
      @multiple-tag-remove='onMultipleTagRemove' />
  </p>
  <p>
    <select-input
      :model-value='["a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b"]'
      multiple
      clearable
      @click='onClick'
      @clear-click='onClearClick'
      @multiple-tag-remove='onMultipleTagRemove' />
  </p>
  <p>
    <select-input
      :model-value='["a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b","a","b"]'
      multiple
      multiple-line
      clearable
      @click='onClick'
      @clear-click='onClearClick' 
      @multiple-tag-remove='onMultipleTagRemove' />
  </p>
</template>

<script setup lang="ts">
import { SelectInput } from 'lc-vue-select-input';
import { ref } from 'vue';
const value = ref('aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa');

const onClick = () => {
  console.log('onClick');
};

const onClearClick = () => {
  console.log('onClearClick');
  
};

const onMultipleTagRemove = (index) => {
  console.log('onMultipleTagRemove', index);
  
};

</script>

<style scoped>

</style>
```

## API

### Attributes

| 属性名 | 说明 | 类型 | 默认值 |
| ---- | ---- | ---- | ---- |
| modelValue | 显示值 | string/array | - |
| placeholder | 提示 | string | 请选择 |
| disabled | 禁用 | boolean | false |
| multiple | 多选 | boolean | false |
| multipleLine | 多选时tag显示多行 | boolean | true |
| clearable | 显示清空icon | boolean | false |

### Events

| 事件名 | 说明 | 类型 |
| ---- | ---- | ---- | 
| click | 点击事件 | ()=>void |
| clear-click | 清空图标点击事件 | ()=>void |
| multiple-tag-remove | 多选tag删除事件 |  (index:number) => void |

### Slots

| 插槽名 | 说明 | 参数 |
| ---- | ---- | ---- | 
| icon | 右侧图标 | - |