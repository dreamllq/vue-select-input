<template>
  <div
    class='el-input el-input--suffix multiple-input'
    :class='{
      "is-disabled": disabled,
      "is-clearable": renderClearIcon
    }'>
    <!-- input --><!-- prepend slot --><!--v-if-->
    <div class='el-input__wrapper' tabindex='-1'>
      <!-- prefix slot --><!--v-if-->
      <input
        v-if='!hasValue'
        class='el-input__inner'
        type='text'
        readonly
        autocomplete='off'
        tabindex='0'
        :placeholder='placeholder'>

      <template v-else>
        <div v-if='!multipleLine' class='el-input__inner multiple-line'>
          <el-tag
            :closable='!disabled'
            type='info'
            class='tag-item'
            @close='onTagRemove(0)'>
            {{ modelValue![0] }}
          </el-tag>
          <template v-if='modelValue!.length>1'>
            <el-tag type='info' class='tag-item-close'>
              +{{ modelValue!.length - 1 }}
            </el-tag>
          </template>
        </div>
        <div v-else class='el-input__inner tags-list'>
          <template v-for='(item, index) in modelValue' :key='index'>
            <el-tag
              :closable='!disabled'
              type='info'
              class='tag-item'
              @close='onTagRemove(index)'>
              {{ item }}
            </el-tag>
          </template>
        </div>
      </template> 
      
      <!-- suffix slot -->
      <span class='el-input__suffix'>
        <span class='el-input__suffix-inner'>
          <span v-if='renderClearIcon' class='clear-btn' @click.stop.prevent='onClearClick'>
            <i class='el-icon-circle-close' />
            <el-icon style='vertical-align: middle;'><circle-close /></el-icon>
          </span>
          <span style='margin-left: 8px;' class='info-btn'>
            <slot name='icon'>
              <el-icon style='vertical-align: middle;'><arrow-down /></el-icon>
            </slot>
          </span>
        </span>
      </span>
    </div><!-- append slot --><!--v-if-->
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { ArrowDown, CircleClose } from '@element-plus/icons-vue';


const props = defineProps({
  modelValue: {
    type: Array,
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
  multipleLine: {
    type: Boolean,
    default: true
  },
  clearable: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['clear-click', 'tag-remove']);

const hasValue = computed(() => Array.isArray(props.modelValue) && props.modelValue.length > 0);
const renderClearIcon = computed(() => props.clearable && !props.disabled && hasValue.value);

const onClearClick = () => {
  emit('clear-click');
};

const onTagRemove = (index) => {
  emit('tag-remove', index);
};
</script>

<style scoped lang="scss">
.multiple-input.is-clearable:not(.is-disabled){
  &:hover {
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
}

.el-input{
  .el-input__inner{
    &.tags-list{
      min-height:  var(--el-input-inner-height);
      height: auto;
      padding: 2px 0;
      position: relative;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      min-width: 0;
      gap: 6px;
    }

    &.multiple-line{
      position: relative;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      min-width: 0;
      gap: 6px;
    }
    ::v-deep(.el-icon){
      vertical-align: middle;
    }
  }
}
</style>