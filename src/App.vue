<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50

#nav
  padding 30px
  a
    font-weight bold
    color #2c3e50
    &.router-link-exact-active
      color #42b983
</style>

<script>
import { EchoServiceClient } from './proto/echo_pb_service';
import { EchoRequest, EchoResponse } from './proto/echo_pb';

export default{
  async created() {
    const request = new EchoRequest();
    request.setMessage('hello');
    const client = new EchoServiceClient('http://127.0.0.1:80');
    client.echo(request, {}, (err, response) => {
      if (err.code === grpc.Code.ok) {
        console.log(response);
      } else {
        Message.error(err.message);
      }
    });
  },
};
</script>
