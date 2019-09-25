<template>
  <div>
    <h2 v-lang>Install</h2><code>npm install @hyjiacan/vue-listpanel</code>
    <p v-lang>or</p><code>yarn add @hyjiacan/vue-listpanel</code>
    <p v-lang>For the latest code, you can:</p><code>git clone https://github.com/hyjiacan/vue-listpanel.git</code>
    <p><span v-lang>or</span> <a href="https://github.com/hyjiacan/vue-listpanel/archive/master.zip"
                                 v-lang>download archive</a></p>
    <h2 v-lang>Source</h2>
    <ul>
      <li><a href="https://github.com/hyjiacan/vue-listpanel.git">Github</a></li>
      <li><a href="https://gitee.com/hyjiacan/vue-listpanel.git">Gitee</a></li>
      <li><a href="https://github.com/hyjiacan/vue-listpanel/blob/master/src/components/Demo.vue" target="_blank"
             v-lang>Demo Source</a></li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'meta-info'
}
</script>
<style lang="less">
html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

::-webkit-scrollbar {
  background-color: rgba(200, 200, 200, .2);
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-thumb {
  background-color: rgba(30, 30, 30, 0.1);
  border-radius: 4px;

  &:hover {
    background-color: rgba(30, 30, 30, 0.2);
  }
}

@media screen and (min-width: 800px) {
}

a, a:visited, a:link, a:active {
  color: #4160aa;
  font-weight: 600;
}

a:focus, a:hover {
  color: #45c153;
}

h1 small {
  font-size: 16px;
  color: #666;
  font-weight: normal;
}

h1 {
  padding: 10px 0;
  border-bottom: solid 3px #AAA;
}

h2 {
  padding: 6px 0;
  border-bottom: solid 2px #CCC;
}

h3 {
  padding: 3px 0;
  border-bottom: solid 1px #EEE;

  & + ul {
    border-left: 3px solid transparent;

    &:hover {
      border-color: #b3b0a9;
    }
  }
}

h1, h2, h3 {
  color: #414448;
  font-weight: normal;
}

li {
  padding: 10px 0;
}

code {
  font-family: Consolas, 'Times New Roman', Times, serif;
  font-size: 13px;
  background-color: #f5f2ea;
  color: #0f5df3;
  line-height: 18px;
  box-sizing: border-box;
  margin: 0 5px;
  padding: 3px 5px;
  border-radius: 3px;
  border: none;
  display: inline;
  box-shadow: 0 0 1px 1px rgba(100, 100, 100, .1);

  &:hover {
    color: #ff9001;
  }
}

main > code {
  padding: 15px 10px;
  margin: 10px 0;
  display: block;
  border-left: 3px solid #b5bdd2;
  box-shadow: none;
  border-radius: 0;
}

@media screen and (max-width: 800px) {
  h1 small {
    display: block;
  }

}

</style>
