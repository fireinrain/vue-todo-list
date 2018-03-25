
<template>
    <div id="footer">
    
        <span>Powered by {{author}},&nbspWelcome to visit my Blog:&nbsp<a href="http://blog.sunriseme.cn">{{blog}}</a></span>
        <br>
        
        <span>Hosted By Github Pages</span>
    </div>
</template>


<script>
export default {
  data: function() {
    return {
      author: "sunriseme",
      blog: "blog.sunriseme.cn"
    };
  }
};
</script>


<style scoped>
#footer {
  margin: 40px;
  text-align: center;
  color: #eee;
  font-size: 15px;
  text-shadow: 0 3 0 2 #eee;
}
#footer a{
    color: #fff;
    text-decoration-line: none;
    text-decoration-style: none;
}
</style>