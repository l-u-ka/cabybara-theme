<template>
  <SfButton
    class="sf-button--pure a-account-icon"
    @click="goToAccount"
  >
    <SfIcon size="xs">
      <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0.5 3.0999C0.4 3.0999 0.199976 3.0999 0.0999756 2.9999C-2.44156e-05 2.8999 0 2.7999 0 2.5999V1.3999C0 1.1999 -2.44156e-05 1.0999 0.0999756 0.999901C0.199976 0.899901 0.4 0.899902 0.5 0.899902H13.5C13.6 0.899902 13.8 0.899901 13.9 0.999901C14 1.0999 14 1.1999 14 1.3999V2.5999C14 2.7999 14 2.8999 13.9 2.9999C13.8 3.0999 13.6 3.0999 13.5 3.0999H0.5ZM0.5 8.0999C0.4 8.0999 0.199976 8.0999 0.0999756 7.9999C-2.44156e-05 7.8999 0 7.7999 0 7.5999V6.3999C0 6.1999 -2.44156e-05 6.0999 0.0999756 5.9999C0.199976 5.8999 0.4 5.8999 0.5 5.8999H13.5C13.6 5.8999 13.8 5.8999 13.9 5.9999C14 6.0999 14 6.1999 14 6.3999V7.5999C14 7.7999 14 7.8999 13.9 7.9999C13.8 8.0999 13.6 8.0999 13.5 8.0999H0.5ZM0.5 13.0999C0.4 13.0999 0.199976 13.0999 0.0999756 12.9999C-2.44156e-05 12.8999 0 12.7999 0 12.5999V11.3999C0 11.1999 -2.44156e-05 11.0999 0.0999756 10.9999C0.199976 10.8999 0.4 10.8999 0.5 10.8999H13.5C13.6 10.8999 13.8 10.8999 13.9 10.9999C14 11.0999 14 11.1999 14 11.3999V12.5999C14 12.7999 14 12.8999 13.9 12.9999C13.8 13.0999 13.6 13.0999 13.5 13.0999H0.5Z" fill="#333333" />
      </svg>
    </SfIcon>
  <!--
    <SfIcon
      icon="account"
      size="xs"
      class="sf-header__icon"
      :class="{
        'sf-header__icon--is-active': isLoggedIn
      }"
    />
    -->
  </SfButton>
</template>

<script>
import { SfIcon, SfButton } from '@storefront-ui/vue';
import { mapGetters, mapActions } from 'vuex';
import { ModalList } from 'theme/store/ui/modals'

export default {
  components: { SfIcon, SfButton },
  computed: {
    ...mapGetters('user', ['isLoggedIn'])
  },
  methods: {
    ...mapActions('ui', {
      openModal: 'openModal'
    }),
    goToAccount () {
      if (this.isLoggedIn) {
        this.$router.push(this.localizedRoute('/my-account'))
      } else {
        this.openModal({ name: ModalList.Auth, payload: 'login' })
      }
    }
  }
};
</script>
