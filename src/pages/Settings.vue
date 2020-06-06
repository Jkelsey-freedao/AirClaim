<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <q-select label="Select Language" v-model="lang" map-options :options="langs" class="row"/>
      <div class="row q-pt-md">Phrase for Success: {{ $t('success') }}</div>
      <div class="row q-pt-md">Phrase for Failure: {{ $t('failed') }}</div>
      <div class="row q-pt-md">Current Language: {{ $i18n.locale }}</div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Settings',
  data() {
    return {
      langs: [
        {
          label: 'German',
          value: 'de'
        },
        {
          label: 'US English',
          value: 'en-us'
        }
      ],
      lang: this.$i18n.locale
    }
  },
  watch: {
    lang(lang) {
      this.$i18n.locale = lang.value
      // set quasar's language too!!
      import(`quasar/lang/${lang.value}`).then(language => {
        this.$q.lang.set(language.default)
      })
    }
  }
}
</script>