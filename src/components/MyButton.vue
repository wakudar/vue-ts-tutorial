<template>
  <button class='primary' @click="onClick">
    <slot></slot>
  </button>
</template>

<script lang="ts">
  import { Component, Emit, Prop, Vue } from 'vue-property-decorator';

  @Component
  export default class MyButton extends Vue {
    private count: number = 0;
    // Props down, Event Up
    // プロパティ: 上位のコンポーネントのデータを下位のコンポーネントで利用する
    @Prop()
    public greet?: string;

    // イベント: コンポーネントで発生した出来事を自身をコンポジションする上位コンポーネントに伝える
    @Emit()
      public myClicked(count: number){
    }

    public onClick() {
      alert(this.greet);
      this.count++;
      this.myClicked(this.count);
    }
  }
</script>