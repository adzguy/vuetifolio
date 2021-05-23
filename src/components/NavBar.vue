<template>
  <div>
    <b-navbar toggleable="sm" type="light" variant="transparent">
      <b-navbar-brand
        ><router-link to="/" class="brand"
          >Vuetifolio</router-link
        ></b-navbar-brand
      >

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="mr-2">
          <b-nav-item
            ><router-link to="/" class="nav-item">Home</router-link></b-nav-item
          >
          <b-nav-item
            ><router-link to="/projects" class="nav-item"
              >Project</router-link
            ></b-nav-item
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<style scoped>
.brand {
  text-transform: uppercase;
  text-decoration: none;
  color: rgb(55, 55, 117);
  font-size: 18px;
  font-weight: 900;
  line-height: 21px;
}

.nav-item {
  text-transform: uppercase;
  text-decoration: none;
  color: rgb(55, 55, 117);
  font-size: 14px;
  font-weight: 700;
  line-height: 21px;
}
</style>
