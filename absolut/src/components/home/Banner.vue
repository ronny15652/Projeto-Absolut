<template>
<div id="fluid" >
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  <div id="main-banner" class="img-fluid">
    <h1>Absoluto</h1>
  </div>
</div>
</template>

<script>
export default {
  name: 'Banner'
}
</script>
<style scoped>
  #main-banner {
      background-image: url('/img/burger.jpg');
      background-position: 0 -250px;
      background-size: cover;
      height: 500px;
      display: flex;
      align-items: center;
      justify-content: flex-start;
  }
  
  #main-banner h1 {
    color: #ffd;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
  }

  .img-fluid {
      max-width: 100%;
      height: auto;
    }
</style>

