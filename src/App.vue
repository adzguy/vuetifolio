<template>
  <body class="d-flex flex-column h-100">
    <div id="app">
      <main class="flex-shrink-0 container mt-5">
        <router-view></router-view>
      </main>
    </div>
    <Footer />
  </body>
</template>

<script>
import Footer from "./components/Footer";
export default {
  name: "App",
  components: { Footer },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 95vh;
  min-height: 600px;
  color: #2c3e50;
  background-color: rgba(0, 0, 255, 0.1);
}
</style>
