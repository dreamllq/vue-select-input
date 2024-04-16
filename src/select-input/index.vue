<template>
  <div class='select-input' :class='{clearable: renderClearIcon,disabled:disabled}' @click='onClick'>
    <multiple-input
      v-if='multiple'
      :model-value='modelValue'
      readonly
      :clearable='clearable'
      :placeholder='placeholder'
      :disabled='disabled'
      :multiple-line='multipleLine'
      @tag-remove='onTagRemove'
      @clear-click='onClearClick'>
      <template #icon>
        <slot name='icon' />
      </template>
    </multiple-input>
    <el-input
      v-else
      :model-value='modelValue'
      readonly
      :placeholder='placeholder'
      :disabled='disabled'
      @change='onChange'
      @update:model-value='onUpdateModelValue'>
      <template #suffix>
        <span v-if='renderClearIcon' class='clear-btn' @click.stop.prevent='onClearClick'>
          <el-icon><circle-close /></el-icon>
        </span>
        <span style='margin-left: 8px;' class='info-btn'>
          <slot name='icon'>
            <el-icon><arrow-down /></el-icon>
          </slot>
        </span>
      </template>
    </el-input>
  </div>
</template>

<script setup lang="ts">
import { PropType, computed } from 'vue';
import { ArrowDown, CircleClose } from '@element-plus/icons-vue';
import MultipleInput from './multiple-input/index.vue';

const props = defineProps({
  modelValue: {
    type: [
      String,
      Number,
      Array
    ] as PropType<any>,
    default: undefined
  },
  placeholder: {
    type: String,
    default: '请选择'
  },
  disabled: {
    type: Boolean,
    default: false
  },
  multiple: {
    type: Boolean,
    default: false
  },
  multipleLine: {
    type: Boolean,
    default: true
  },
  clearable: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits([
  'update:modelValue',
  'change',
  'click',
  'clear-click',
  'multiple-tag-remove'
]);

const hasValue = computed(() => props.modelValue && props.modelValue !== '');
const renderClearIcon = computed(() => props.clearable && !props.disabled && hasValue.value);

const onUpdateModelValue = (val) => {
  emit('update:modelValue', val);
};

const onChange = (...args) => {
  emit('change', ...args);
};

const onClick = (...args) => {
  if (props.disabled) return;
  emit('click', ...args);
};

const onClearClick = (...args) => {
  if (props.disabled) return;
  emit('clear-click', ...args);
};

const onTagRemove = (index) => {
  emit('multiple-tag-remove', index);
};

</script>

<style scoped lang="scss">
.select-input {
  width: 100%;

  ::v-deep(.el-input) {
    .el-input__inner,.el-input__suffix-inner {
      cursor: pointer;
    }
  }

  ::v-deep(.el-input) {
    &.is-disabled {
      .el-input__inner,.el-input__suffix-inner {
        cursor: not-allowed;
      }

      .el-input__suffix-inner i {
        color: var(--el-input-placeholder-color);
      }
    }
  }

  &.clearable:not(.disabled):hover {
    .clear-btn {
      display: inline;
    }
    .info-btn{
      display: none;
    }
  }

  .clear-btn {
    display: none;
  }

  ::v-deep(.el-icon){
    vertical-align: middle;
  }
}
</style>