<template>
  <div class="column justify-center items-center" id="row-container">
    <q-card class="my-card">
      <q-card-section style="text-align: center">
        <div v-if='authState && authState.isAuthenticated'>
          <h6 v-if="claims && claims.email">You are logged in as {{ claims.email }}</h6>
          <h6 v-else>You are logged in</h6>
          <q-btn flat color="primary" @click="todo">Go to Todo app</q-btn>
          <q-btn flat @click="logout">Log out</q-btn>
        </div>
        <div v-else>
          <h6>Please <a href="#" @click.prevent="login">log in</a> to access Todo app</h6>
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>

<script>


</script>