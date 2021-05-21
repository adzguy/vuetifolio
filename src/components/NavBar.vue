<template>
  <div>
    <b-navbar toggleable="sm" type="light" variant="transparent">
      <b-navbar-brand>Vuetifolio</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item><router-link to="/">Home</router-link></b-nav-item>
          <b-nav-item
            ><router-link to="/projects">Project</router-link></b-nav-item
          >
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

