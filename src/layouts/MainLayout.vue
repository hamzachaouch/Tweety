<template>
  <q-layout view="lHr LpR fFf">
    <q-header reveal bordered class="bg-primary text-white">
      <q-toolbar>
        <q-btn
          dense
          flat
          round
          color="dark"
          icon="menu"
          @click="left = !left"
        />

        <q-toolbar-title class="absolute-center">
          <q-avatar>
            <img src="tweety.png" />
          </q-avatar>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="left" side="left" bordered>
      <h4 class="text-dark q-ml-md q-mt-xs">Tweety</h4>
      <h5 style=" margin: -30px 20px;">Contacts</h5>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {
      left: false,
      right: false
    };
  }
};
</script>
<style lang="css" scoped></style>
