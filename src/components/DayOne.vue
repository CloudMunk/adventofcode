<template>
  <div class="hello">
      <router-link to="/dayone"><h1>Day One</h1></router-link>
      <router-link to="/daytwo"><h1>Day Two</h1></router-link>
      <router-link to="/daythree"><h1>Day Three</h1></router-link>
      <router-link to="/dayfour"><h1>Day Four</h1></router-link>

  </div>
</template>

<script>
export default {
  name: 'DayOne',
  props: {
    msg: String
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
