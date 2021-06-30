<template>
  <form>
    <slot></slot>
  </form>
</template>

<script>
export default {
  name: 'myForm',
  props: {
    model: {
      type: Object
    },
    rules: {
      type: Object
    }
  },
  provide() {
    return {
      form: this
    }
  },
  data() {
    return {
      fields: []
    };
  },
  // vue组件的渲染顺序是由内而外的，所以item组件会比form组件先渲染，在item组件里 mouted生命周期派发事件，
  // 在form组件如果在mouted上监听是监听不到的，需要将事件监听放在created中，form的created会比item的mouted早
  created() {
    this.$on('on-form-item-add', (field) => {
      console.log('on-form-item-add on field', field);
      if (field) this.fields.push(field);
    });
    this.$on('on-form-item-remove', (field) => {
      if (field.prop) this.fields.splice(this.fields.indexOf(field), 1);
    });
  },
  methods: {
    // 公开方法： 全部重置数据
    resetFields() {
      this.fields.forEach(field => {
        field.resetField();
      });
    },
    // 公开方法： 全部校验数据,支持promise
    validate(callback) {
      return new Promise(resolve => {
        let valid = true;
        let count = 0;
        this.fields.forEach(field => {
          field.validate('', errors => {
            if (errors) {
              valid = false;
            }
            if (++count === this.fields.length) {
              // 全部完成
              resolve(valid);
              if (typeof callback === 'function') {
                callback(valid);
              }
            }
          });
        });
      });
    }
  }
};
</script>

<style>

</style>
