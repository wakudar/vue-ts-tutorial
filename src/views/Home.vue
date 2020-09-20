<template>
  <div class="home">
    <!-- 発火されたメソッドは、@clicked='callbackMethod'という形でイベントハンドラの登録を行う -->
    <p>{{ greetText }}</p>
    <p>挨拶した回数: {{ count }}回</p>
    <p v-if="isRegulars">いつもありがとうございます。</p>
    <p><MyButton class='my-button' :greet="greetText" @my-clicked="onMyButtonClicked">挨拶する</MyButton></p>
    <p><ResetButton v-model="greetText"></ResetButton></p>
  </div>
</template>

<script lang="ts">
import { Component, Watch, Vue } from 'vue-property-decorator';
import MyButton from '@/components/MyButton.vue'; // @ is an alias to /src
import ResetButton from '@/components/ResetButton.vue';

@Component({
  components: {
    MyButton,
    ResetButton,
  },
})
export default class Home extends Vue {
  private count: number = 0;
  public greetText: string = "Hello";

  // 算出プロパティ: getterを使って記述
  public get isRegulars(): boolean {
    return this.count >= 5;
  }

  // Watch
  @Watch('count')
  public countChange() {
    if(this.count === 5) {
      alert('常連になりました');
    }
  }

  public onMyButtonClicked(count: number) {
    this.count = count;
    this.greetText = "こんにちは";
  }
}
</script>
