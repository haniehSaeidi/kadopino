<script>
  import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'
  import camelCase from 'lodash/camelCase'

  export default {
    components: {
      FontAwesomeIcon,
    },
    props: {
      source: {
        type: String,
        default: 'font-awesome',
      },
      name: {
        type: String,
        required: true,
      },
    },
    computed: {
      fontAwesomeIcon() {
        return {
          user: require('@fortawesome/free-solid-svg-icons/faUser').definition,
          phone: require('@fortawesome/free-solid-svg-icons/faPhone').definition,
          lock: require('@fortawesome/free-solid-svg-icons/faLock').definition,
        }[this.name]
      },
      customIconClass() {
        return this.$style[camelCase('icon-custom-' + this.name )]
      },
    },
  }
</script>

<template>
  <FontAwesomeIcon
    v-if="source === 'font-awesome'"
    :icon="fontAwesomeIcon"
    class="fas fa-fw"
    v-bind="$attrs"
  />
  <span
    v-else-if="source === 'custom'"
    :class="customIconClass"
  />
</template>