<template>
  <s-button :class="['app-logo', { responsive }]" type="link" size="large" v-on="$listeners">
    <polkaswap-logo :theme="theme" class="app-logo__image" />
  </s-button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Theme from '@soramitsu/soramitsu-js-ui/lib/types/Theme';

import PolkaswapLogo from '@/components/logo/Polkaswap.vue';

@Component({
  components: {
    PolkaswapLogo,
  },
})
export default class AppLogoButton extends Vue {
  @Prop({ default: Theme.LIGHT, type: String }) theme!: Theme;
  @Prop({ default: false, type: Boolean }) responsive!: boolean;
}
</script>

<style lang="scss" scoped>
$logo-full-width: 172px;
$logo-full-height: 46px;

.app-logo {
  background-size: cover;
  width: $logo-full-width;
  height: $logo-full-height;
  border-radius: 0;

  &.el-button {
    padding: 0;
    margin-left: 0;
    margin-right: 0;
    transition-duration: 0s;
  }

  &.responsive {
    background-image: url('~@/assets/img/pswap.svg');
    width: var(--s-size-medium);
    height: var(--s-size-medium);

    @include tablet {
      background-image: none;
      width: $logo-full-width;
      height: $logo-full-height;
    }

    .app-logo__image {
      visibility: hidden;

      @include tablet {
        visibility: visible;
      }
    }
  }
}
</style>
