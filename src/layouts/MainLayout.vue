<template>
  <q-layout view="hHh lpR fFf">

    <q-header class="bg-grey-3 text-primary" style="box-shadow: inherit">
      <q-toolbar class="q-container">
        <q-toolbar-title>
            <img src="~assets/logo.png" class="q-py-md" style="max-width: 210px">
        </q-toolbar-title>
        <q-space />
        <q-tabs v-model="tab" shrink>
          <q-tab name="tab1" label="Tab 1" />
          <q-tab name="tab2" label="Tab 2" />
          <q-tab name="tab3" label="Tab 3" />
        </q-tabs>
      </q-toolbar>

    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="bg-grey-3">
      <q-toolbar class="q-container">
          <img src="~assets/logo.png" class="q-py-md" style=" margin:auto; max-width: 210px">
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
export default {
  data () {
    return {
    }
  }
}
</script>
