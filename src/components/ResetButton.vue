<template>
  <button @click="onClick">Reset</button>
</template>

<script lang="ts">
  import { Component, Prop, Emit, Vue } from 'vue-property-decorator';

  @Component
  export default class ResetButton extends Vue {
    // initialValue
    private initialValue!: string;

    /* モデルバインド(v-model) .. バインドされた値はコンポーネントが変更することがあると宣言すること */
    // モデルバインドするときはvalueとinputを定義する必要がある
    // モデルバインドのために記述必須(value)
    @Prop()
    public value!: string;

    /* ライフサイクルフック（created: 生成された瞬間に呼び出される） */
    public created() {
      this.initialValue = this.value;
    }

    // モデルバインドのために記述必須(input())
    @Emit()
    public input(value: string) {
    }

    // onClick()
    public onClick() {
      this.input(this.initialValue);
    }
  }
</script>