<template>
  <div id="app">
    <header>
      <div class = "top-header">
        Yusuke's Programming Learning<span>制作日：2020/6/25</span>      
      </div>
      </header>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

header{
  font-size:2.5vw;
  height:80px;
  background-color:rgb(226, 229, 229);
  border-bottom:2px solid rgb(118, 118, 119);
  line-height:80px;
  text-align:left;
  padding-left:10%;
  margin-bottom:60px;
}

.top-header span{
  font-size: 1.4vw;
  position:absolute;
  right:5%;
  top:2%;
}
</style>
