<script>
export default {
  name: "Navbar",
  props: ["currentUser"]
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <p class="navbar-brand">Todo</p>

    <div v-if="currentUser" class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item active">
          <p class="nav-link">
            Home
            <span class="sr-only">(current)</span>
          </p>
        </li>

        <li class="nav-item">
          <p v-on:click="$emit('on-logout' )" class="nav-link">logout</p>
        </li>
      </ul>
    </div>
    <div v-else class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item active">
          <p v-on:click="$emit('change-auth' , 'signin' )" class="nav-link">
            SignIn
            <span class="sr-only">(current)</span>
          </p>
        </li>

        <li class="nav-item">
          <p v-on:click="$emit('change-auth' , 'register' )" class="nav-link">Register</p>
        </li>
      </ul>
    </div>
  </nav>
</template>
