<template>
  <footer class="o-footer">
    <div class="top-footer">
      <div class="discount">
        <h2 class="discount-head">Get Our Special Discount</h2>
        <p class="discount-mid">Donec eu tristique felis. Duis augue mi, auctor ut purus et, dignissim aliquet quam. 
          register your email for news and special offers</p>
        <div class="email">
          <input type="email" placeholder="Email adress ..." class="email-input"/>
          <SfButton>Get Coupon Now</SfButton>
        </div>
      </div>
      <SfImage
        src="../../assets/Clients.png"
        alt="clients"
      />
    </div>
    <div class="mid-footer">
      <p class="mid-footer-p">We’re confident we’ve provided all the best for you. Stay connect with us</p>
      <div class="mid-footer-img">
        <SfImage
          src="../../assets/socials.png"
          alt="socials"
          class="image"
        />
      </div>
      <div class="mid-footer-blank">&nbsp</div>
    </div>
    <SfFooter :column="4" :multiple="true" class="sf-footer">
      <SfFooterColumn
        v-for="linkGroup in links"
        :key="linkGroup.name"
        :title="$t(linkGroup.name)"
      >
        <SfList>
          <SfListItem v-for="link in linkGroup.children" :key="link.name">
            <router-link v-if="link.link" :to="localizedRoute(link.link)" exact>
              <SfMenuItem class="sf-footer__menu-item" :label="$t(link.name)" />
            </router-link>
            <SfMenuItem
              v-else-if="link.clickHandler"
              class="sf-footer__menu-item"
              :label="$t(link.name)"
              @click="link.clickHandler"
            />
          </SfListItem>
        </SfList>
      </SfFooterColumn>
      <SfFooterColumn :title="$t('Contact Info')">
        <SfImage
          src="../../assets/contact.png"
          alt="contact-img"
          class="sf-footer__img"
        />
      </SfFooterColumn>
    </SfFooter>
    <div class="bottom-footer">
      <p class="bottom-footer-p">Copyright 2017 RenoshopBee all right reserved  -  Design by BeeStudios</p>
      <div class="bottom-footer-img">
        <SfImage
          src="../../assets/card.png"
          alt="card"
        />
      </div>
    </div>
    <ABackToTop bottom="20px" right="20px" visibleoffset="200" class="desktop-only" />
  </footer>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';
import ABackToTop from 'theme/components/atoms/a-back-to-top';
import { SfFooter, SfList, SfMenuItem, SfImage, SfInput, SfButton } from '@storefront-ui/vue';
import { ModalList } from 'theme/store/ui/modals'
import { getPathForStaticPage } from 'theme/helpers';
import config from 'config';
import { currentStoreView } from '@vue-storefront/core/lib/multistore';
import get from 'lodash-es/get';

export default {
  name: 'OFooter',
  components: {
    ABackToTop,
    SfFooter,
    SfList,
    SfMenuItem,
    SfImage,
    SfInput,
    SfButton
  },
  data () {
    return {
      social: ['facebook', 'pinterest', 'twitter', 'youtube']
    };
  },
  computed: {
    ...mapGetters('user', ['isLoggedIn']),
    multistoreEnabled () {
      return get(config, 'storeViews.multistore', false);
    },
    getVersionInfo () {
      return `v${process.env.__APPVERSION__} ${process.env.__BUILDTIME__}`;
    },
    currentLanguage () {
      const { i18n = config.i18n } = currentStoreView();
      return `${i18n.defaultCountry} / ${i18n.defaultLanguage} / ${i18n.currencyCode}`;
    },
    links() {
      return {
        information: {
          name: 'INFORMATION',
          children: [
            { name: 'Delivery Information', link: '/delivery' },
            { name: 'Discount', link: '/discount' },
            { name: 'Sitemap', link: '/store-locator' },
            { name: 'Privacy Policy', link: '/privacy' },
            {
              name: 'My account',
              ...this.isLoggedIn
                ? { link: '/my-account' }
                : { clickHandler: () => this.openModal({ name: ModalList.Auth, payload: 'login' }) }
            }
          ]
        },
        myAccount: {
          name: 'MY ACCOUNT',
          children: [
            { 
              name: 'Sign In',
              ...this.isLoggedIn
                ? { link: '/sign-in' }
                : { clickHandler: () => this.openModal({ name: ModalList.Auth, payload: 'login' }) }
            },
            { name: 'View Cart', link: '/cart' },
            { name: 'My Wishlist', link: '/wish-list' },
            { name: 'Check Out', link: '/check-out' },
            { name: 'Track My Order', link: '/order' }
          ]
        },
        help: {
          name: 'HELP',
          children: [
            { name: 'F.A.Q', link: '/faq' },
            { name: 'Shipping', link: '/shipping' },
            { name: 'Contact Us', link: '/contact' },
            { name: 'Privacy Policy', link: '/privacy' }
          ]
        }
      }
    }
  },
  methods: {
    ...mapActions('ui', {
      openModal: 'openModal'
    }),
    showLanguageSwitcher () {
      this.openModal({ name: ModalList.LanguageSwitcher })
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~@storefront-ui/shared/styles/helpers/breakpoints";

.top-footer {
  display:grid;
  grid-template-columns: 1fr 1fr;
}

.discount {
  background-image: url("../../assets/Group.png");
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.discount-head {
  color: white;
  margin: 0;
}
.discount-mid {
  font-size: 0.7em;
  color: white;
  font-weight:500;
  max-width: 70%;
  text-align: center;
}

.email {
  display: grid;
  grid-template-columns: 60% 40%;
  width: 80%;
}
.email-input {
  margin-right: 0.5rem;
}

.mid-footer {
  padding: 0;
  align-items: center;
  display: grid;
  grid-template-columns: 4fr 1fr 1fr;
  text-align: center;
}
.mid-footer-p {
  font-size: 1em;
  font-weight: 300;
  border-bottom: 1px solid rgba(128, 128, 128, 0.3);
  border-right: 1px solid rgba(128, 128, 128, 0.3);
  font-size: 0.8em;
}
.mid-footer-img {
  border-bottom: 1px solid rgba(128, 128, 128, 0.3);
  border-right: 1px solid rgba(128, 128, 128, 0.3);
}
.mid-footer-blank {
  border-bottom: 1px solid rgba(128, 128, 128, 0.3);
}

.mid-footer-p, .mid-footer-img, .mid-footer-blank {
  height: 1.5rem;
  padding: 0.5rem 0.5rem;
}

.sf-footer__img {
  margin-top: 1.5rem;
}

.sf-footer {
  margin: 0 12rem;
}

.bottom-footer {
  height: 3rem;
  display: flex;
  background-color: black;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 12rem;
}

.bottom-footer-p {
  color: rgba(128, 128, 128, 0.5);
  font-size: 0.8em;
  font-weight: bold;
}

.o-footer {
  @include for-desktop {
    max-width: 1272px;
    margin: auto;
  }
  .sf-footer {
    --footer-width: auto;
  }
}
.social-column {
  flex-basis: auto;
}
.social-icon {
  padding: var(--spacer-sm) var(--spacer-xl);
  @include for-desktop {
    padding: var(--spacer-xs) 0;
  }
  &__img {
    height: 1.75rem;
    &:not(:last-child) {
      margin-right: var(--spacer-base);
    }
  }
}
</style>
