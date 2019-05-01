<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <select 
     :value="value"
     @change="updateValue"
     v-bind="$attrs">
       <option v-for="option in options"
       :selected="option === value"
       :value="option"
       :key="option">
       {{ option }}
       </option> 
    </select>
  </div>
</template>

<script>
export default {
  inheritAttrs: false,
  props: {
    options: {
      type: Array,
      required: true
    },
    value: [String, Number],
    label: String
  },
  methods: {
    updateValue(event) {
      // inputイベントを発火
      // 理由：親コンポーネントにてinputイベントをキャッチさせるため
      // 背景：親コンポーネントではv-modelプロパティを定義
      //      v-modelを定義すること=v-bind:valueと@inputを定義になる
      //      そのためこのコンポーネント内でinputイベントを発火させる必要がある
      this.$emit('input', event.target.value)
    }
  },
}
</script>
