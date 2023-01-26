<template>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

    <title>Covid Tacking</title>
    <meta name="description" content="una pagina en la cual podremos ver estadistica sobre el covid">
    <meta name="author" content="Kenlly Chacon">
    <meta name="keywords" content="covid, piases, us, estadistica, casos">
    <meta name="google-site-verification" content="">
    <meta name="googlebot" content="">
  </head>


  <body>
  <header>
  </header>

  <nav>
  </nav>

  <section>
    <CovidTracking/>
  </section>

  <footer>
    Derechos Reservados 2023-2024
  </footer>

  </body>
</template>

<script>
import CovidTracking from "@/components/CovidTracking.vue";
export default {
  name: "Principal",
  components:{
    CovidTracking
  }
}
</script>

<style scoped>

header,nav,section,footer,aside,article{
  display: block;
}

h1{
  margin: 25px;
  text-align: center;
}

footer{
  font-size: 18px;
  margin: 50px auto;
  clear: both;
  text-align: center;
}

body{
  background-color: #1B1F27;
}

</style>