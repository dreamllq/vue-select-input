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
      :multiple-line='false'
      clearable
      @click='onClick'
      @clear-click='onClearClick' 
      @multiple-tag-remove='onMultipleTagRemove' />
  </p>
</template>

<script setup lang="ts">
import { SelectInput } from '@/index.ts';
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