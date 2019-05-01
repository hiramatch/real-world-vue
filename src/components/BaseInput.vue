<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <input 
     :value="value"
     @input="updateValue"
     type="text">
  </div>
</template>

<script>
export default {
  props: {
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
