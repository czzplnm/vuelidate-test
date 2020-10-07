<template>
  <div class="form-group">
    <div class="label-wrapper">
      <label>{{ label }}</label>
    </div>
    <div class="input-button-wrapper">
      <input :type="type"
             class="form-control"
             :name="name"
             :value="modelValue"
             :aria-label="label"
             @input="setValue($event)"
      />
    </div>

    <div :visible="$v[this.name].$error">
      <p v-for="$error in $v[this.name].$errors" :key="$error.$property">
        {{ $error.$message }}
      </p>
    </div>
  </div>
</template>

<script lang="ts">
  import {VuelidateMixin} from '@vuelidate/core'

  export default {
    name: 'InputTemplate',
    mixins: [VuelidateMixin],
    validations(): object {
      console.log('Accessing validations', this.rules);
      return this.rules;
    },
    props: {
      //validation rules
      name: {
        type: String,
        required: true,
      },
      rules: {
        type: Object,
        required: true
      },
      type: {
        default: 'text'
      },
      label: {
        type: String,
        required: true
      },
      modelValue: {
        type: String,
        required: false
      },
    },
    methods: {
      setValue($event: any) {
        this.$emit('update:modelValue', $event.target.value)
      },
    }
  }
</script>

<style scoped>
  .form-group {
    width: 100%;
    text-align: center;
  }

  input {
    width: 80%;
    font-weight: bold;
  }
</style>