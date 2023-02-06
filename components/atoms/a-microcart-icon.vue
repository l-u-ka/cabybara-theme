<template>
  <SfButton
    class="sf-button--pure a-microcart-icon"
    @click="openMicrocart"
  >
    <SfIcon size="xs">
      <svg width="10" height="10" viewBox="0 0 18 16" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M16.5 9.4C16.5 9.6 16.4 9.7 16.2 9.8C16.1 9.9 15.9 10 15.8 10H6.59998L6.80005 11H15.2C15.4 11 15.6 11.1 15.8 11.3C15.9 11.5 16 11.7 15.9 11.9L15.7 12.7C16.1 12.8 16.3 13 16.5 13.3C16.7 13.6 16.8 13.9 16.8 14.3C16.8 14.7 16.6 15.1 16.2 15.5C15.9 15.8 15.5 16 15 16C14.5 16 14.1 15.8 13.8 15.5C13.4 15.1 13.2 14.7 13.2 14.2C13.2 13.7 13.4 13.3 13.8 13H7.19995C7.59995 13.3 7.69995 13.7 7.69995 14.2C7.69995 14.7 7.59995 15.1 7.19995 15.5C6.89995 15.8 6.5 16 6 16C5.5 16 5.10005 15.8 4.80005 15.5C4.40005 15.1 4.19995 14.7 4.19995 14.3C4.19995 13.9 4.3 13.6 4.5 13.4C4.6 13.1 4.89998 12.9 5.09998 12.7L2.90002 2H0.699951C0.499951 2 0.399951 1.9 0.199951 1.8C0.0999512 1.6 0 1.5 0 1.3V0.800003C0 0.500003 0.0999512 0.399997 0.199951 0.199997C0.399951 0.0999969 0.499951 0 0.699951 0H4C4.1 0 4.30002 0.0999969 4.40002 0.199997C4.60002 0.299997 4.59995 0.399998 4.69995 0.599998L5 2H17.2C17.5 2 17.7 2.1 17.8 2.3C18 2.5 18 2.7 18 2.9L16.5 9.4Z" fill="#333333" />
      </svg>
      <template #badge>
        <SfBadge v-show="!floatingIcon && totalQuantity" class="sf-icon__badge sf-badge--number">
          {{ totalQuantity }}
        </SfBadge>
      </template>
    </SfIcon>
  <!--
    <SfIcon
      size="xs"
      :icon="floatingIcon ? 'add_to_cart' : 'empty_cart'"
      :class="floatingIcon ? 'sf-bottom-navigation__floating-icon' : 'sf-header__icon'"
      :aria-label="$t('Open microcart')"
    >
      <template #badge>
        <SfBadge v-show="!floatingIcon && totalQuantity" class="sf-icon__badge sf-badge--number">
          {{ totalQuantity }}
        </SfBadge>
      </template>
    </SfIcon>
    -->
  </SfButton>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';
import { SfIcon, SfButton, SfBadge } from '@storefront-ui/vue';

export default {
  components: { SfIcon, SfButton, SfBadge },
  props: {
    floatingIcon: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    ...mapGetters({
      totalQuantity: 'cart/getItemsTotalQuantity'
    })
  },
  methods: {
    ...mapActions({
      openMicrocart: 'ui/toggleMicrocart'
    })
  }
};
</script>

<style lang="scss" scoped>
.a-microcart-icon {
  position: relative;
  .sf-header__icon {
    cursor: pointer;
  }
}
</style>
