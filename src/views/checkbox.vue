<template>
  <div>
      <h3>组合多选框组件——CheckboxGroup & Checkbox</h3>

      <my-checkbox v-model="single">单独选项</my-checkbox>

      <br>
      数据：{{ single }}

      <br><br>

      <my-checkbox-group v-model="multiple">
          <my-checkbox label="option1">选项 1</my-checkbox>
          <my-checkbox label="option2">选项 2</my-checkbox>
          <my-checkbox label="option3">选项 3</my-checkbox>
          <my-checkbox label="option4">选项 4</my-checkbox>
      </my-checkbox-group>

      <br>
      数据：{{ multiple }}
  </div>
</template>
<script>
  import myCheckboxGroup from '../components/checkbox/checkbox-group.vue';
  import myCheckbox from '../components/checkbox/checkbox.vue';
  export default {
      components: { myCheckboxGroup, myCheckbox },
      data () {
          return {
              single: false,
              multiple: ['option1']
          }
      }
  }
</script>