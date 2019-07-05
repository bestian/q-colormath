<template lang="pug">
  q-layout(view='lHh Lpr lFf')
    q-header(elevated='')
      q-toolbar
        q-btn(flat='', dense='', round='', @click='leftDrawerOpen = !leftDrawerOpen', aria-label='Menu')
          q-icon(name='menu')
        q-toolbar-title
          | {{ $t($route.path) }}
        .q-gutter-md
          q-select(v-model='$i18n.locale', :options='langs', :label="$t('lang')", emit-value='')
    q-drawer(v-model='leftDrawerOpen', bordered='', content-class='bg-grey-2')
      q-list
        q-item(clickable='', @click.native="$router.push('/')", v-ripple='')
          q-item-section(avatar='')
            q-icon(name='home')
          q-item-section
            | {{$t('home')}}
        q-item-label(header='') {{$t('game')}}
        q-item(clickable='', @click.native="$router.push('/m_color')", v-ripple='')
          q-item-section(avatar='')
            q-icon(name='format_color_fill')
          q-item-section
            | {{$t('m_color')}}
        q-item(clickable='', @click.native="$router.push('/aladin')", v-ripple='')
          q-item-section(avatar='')
            q-icon(name='repeat')
          q-item-section
            | {{$t('aladin')}}
        q-item-label(header='') {{$t('setting')}}
        q-item
          q-color.my-picker(v-model='rgb', inline='')
    q-page-container
      router-view(:rgb='rgb')

</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'MyLayout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      langs: [
        { label: '繁體中文', value: 'zh-TW' },
        { label: '簡体中文', value: 'zh-CN' },
        { label: 'US English', value: 'en-us' }
      ],
      rgb: '#af0'
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
  body {
    font-size: 22px;
  }

  .column {
    text-align: left !important;
  }
</style>
