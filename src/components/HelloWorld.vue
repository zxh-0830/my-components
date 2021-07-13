<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
    <video id="myVideo" preload="auto" width="400px" height="600px" controls muted src="http://upmov.a.yximgs.com/upic/2021/07/08/11/BMjAyMTA3MDgxMTQxMTFfMjI2MjE3MDI5NV81MjgyNTE2NjYxM18yXzM=_b_Baa681aebc0a9e0854a5a88136565edff.mp4?tag=1-1625716594-unknown-0-vnlsjbmlb7-e567c08c0f06e63d&clientCacheKey=3xct4uz2w6hb2ig_b.mp4&tt=b&di=ca5a16ee&bp=13290"></video>
    <video id="myVideo2" width="400px" height="600px" preload="auto" controls muted src="https://s3-gjzc.my.99.com/pre-creation-zone/video/60eba48201aa850032c5bc85.mp4"></video>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted() {
    this.getMyVideo();
  },
  methods: {
    getMyVideo() {
      const video = document.getElementById('myVideo2');
      // console.log('myVideo', video.controlsList);
      // console.log('networkState', video.networkState);
      setTimeout(function(){
            // console.log(video.networkState);//1
        },200);
    //   video.addEventListener('loadedmetadata', function(e) {
    //   console.log('提示视频的元数据已加载')
    //   console.log(e)
    // });
    // video.addEventListener('loadeddata', function(e) {
    //   console.log('提示当前帧的数据是可用的')
    //   console.log(e)
    // })
    video.addEventListener("progress", function() {
      console.log('progress1');
　　if (Math.round(video.buffered.end(0)) / Math.round(video.seekable.end(0)) === 1) {
      console.log('progress2');
　　}
　　}, false);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
