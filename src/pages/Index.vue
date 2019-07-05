<template>
  <q-page class="flex flex-center">
    <img :alt="$t('start')" src="~assets/Icon.png" @click = "$router.push('/m_color')"/>
  </q-page>
</template>

<style>
  img {
    width: 100%;
  }
</style>

<script>
export default {
  name: 'PageIndex'
}
</script>
