<template>
  <section class="container">
    <div>
      <div class="row">
        <br/>
      </div>
      <div class="row">
        <div class="col-sm-12">
          <h1 class="title">
            暗号メーカー<br/>〜ango!〜
          </h1>
          <br/>
          <h2 class="subtitle">
            暗号を作成して、Twitterに投稿しよう！
          </h2>
        </div>
      </div>

      <div class="row">
        <div class="col-sm-12">
          <h3 class="ango-title">
            ◆シャッフル暗号
          </h3>
          <h4 class="ango-description">
            単純にシャッフルするだけです。<br/>
            ※まずはここから
          </h4>
          <textarea id="from-string" class="form-control" rows="3" placeholder="暗号前の文字列" v-model="fromString" v-on:keyup="changeFromString" v-on:change="changeFromString"/>
          <br/>
          ⬇暗号化⬇<br/>
          <br/>
          <textarea id="to-string" class="form-control" rows="10" placeholder="暗号後の文字列" v-model="toString" />
        </div>
      </div>
      <div class="row">
        <div class="col-sm-3">
          <a class="btn mt-3 btn-primary" :href="twUrl" target="_blank">
            <i class="fab fa-twitter"/>
            ツイート
          </a>
        </div>
      </div>
      <div class="row">
        <br/>
      </div>
    </div>
  </section>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },

  data: function(){
      return {
      	  // Twitterのシェア用URL
          twUrl: '',
          fromString: '',
          toString: '',
      }
  },
  methods: {

    changeFromString: function(){
      var fromString = this.fromString.split(/\r\n|\r|\n/);
      var toString = [];
      var ret = '';
      fromString.forEach(str => {
        toString.push(this.ango(str));
      });
      var idx = 0;
      toString.forEach(str => {
        if(idx != 0){
          ret += '\r\n';
        }
        ret += str;
        idx++;
      });
      this.toString = ret;
      this.createSnsUrl();
    },

    ango: function(str){
      var ret = '';
      var strs = str.split('');
      ret = this.angoShuffle(strs);
      return ret;
    },

    /**
     * シャッフル暗号
     */
    angoShuffle: function(array){
      var i;
      var ret = '';
      for (i=0 ; i<array.length; i++){
        var tmpA, tmpB, rnd;
        rnd = Math.floor(Math.random() * array.length);
        tmpA = array[i];
        tmpB = array[rnd];
        array[i] = tmpB;
        array[rnd] = tmpA;
      }
      for (i=0 ; i<array.length; i++){
        ret += array[i];
      }

      return ret;
    },

    /**
     * シェア用のURLを作成します。
     */
    createSnsUrl: function(){
      // 現在のurlをエンコード
    	var url = encodeURIComponent(location.href);
    	// ページ文言
      var txt = encodeURIComponent(this.toString);
      // ハッシュタグ
      var hashtag = encodeURIComponent("#暗号メーカー");
    	// Twitter用のurl作成 ハッシュタグもtxtを使用
      this.twUrl = 'https://twitter.com/intent/tweet?text=' + txt + '%0a%0a' + hashtag + '%0a&url=' + url;
    }
  },
  mounted: function () {
    this.createSnsUrl();
  },
  watch: { 
      // 画面切り替え時
      '$route' (to, from) {
          this.createSnsUrl();
      }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  min-height: 20vh;
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-size: 64px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  min-height: 10vh;
  font-weight: 300;
  font-size: 36px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.ango-title {
  font-weight: 300;
  font-size: 36px;
  word-spacing: 5px;
  padding-bottom: 15px;
  text-align: left;
}

.ango-description {
  font-weight: 300;
  font-size: 16px;
  word-spacing: 5px;
  padding-bottom: 15px;
  text-align: left;
}

.links {
  padding-top: 15px;
}
</style>
