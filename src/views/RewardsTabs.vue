<template>
  <div class="container rewards-tabs">
    <s-tabs :value="currentTab" type="card" @input="handleChangeTab">
      <s-tab
        v-for="rewardsTab in RewardsTabsItems"
        :key="rewardsTab"
        :label="t(`rewards.${rewardsTab}`)"
        :name="rewardsTab"
      />
    </s-tabs>
    <component :is="currentTab" :parent-loading="parentLoading" />
  </div>
</template>

<script lang="ts">
import { Component, Mixins } from 'vue-property-decorator';
import { mixins } from '@soramitsu/soraneo-wallet-web';

import TranslationMixin from '@/components/mixins/TranslationMixin';
import { PageNames, RewardsTabsItems } from '@/consts';
import router, { lazyView } from '@/router';

@Component({
  components: {
    Rewards: lazyView(PageNames.Rewards),
    ReferralProgram: lazyView(PageNames.ReferralProgram),
  },
})
export default class RewardsTabs extends Mixins(mixins.LoadingMixin, TranslationMixin) {
  readonly RewardsTabsItems = RewardsTabsItems;

  get currentTab(): string {
    return this.$route.name as string;
  }

  handleChangeTab(name: string): void {
    router.push({ name });
  }
}
</script>

<style lang="scss">
$rewards-tabs-height: 72px;

.rewards-tabs {
  &.container {
    padding-top: 0;
    padding-right: 0;
    padding-left: 0;
    .s-tabs {
      background-color: inherit;
      &,
      .el-tabs__header,
      .el-tabs__nav-wrap,
      .el-tabs__active-bar {
        border-top-right-radius: inherit;
        border-top-left-radius: inherit;
      }
    }
    .el-tabs__header,
    .el-tabs__nav {
      width: 100%;
    }
    .el-tabs__header .el-tabs {
      &__nav,
      &__nav-wrap,
      &__item {
        height: $rewards-tabs-height;
        line-height: $rewards-tabs-height;
      }
      &__nav {
        .el-tabs__item {
          width: 50%;
        }
      }
      &__nav-wrap {
        .el-tabs__item {
          &,
          &.is-active {
            @include page-header-title(true);
            border-top-right-radius: 0;
            border-top-left-radius: inherit;
          }
          &:last-child {
            border-top-right-radius: inherit;
            border-top-left-radius: 0;
          }
        }
      }
    }
    .s-tabs + * {
      padding-top: $inner-spacing-big;
      padding-right: $inner-spacing-big;
      padding-left: $inner-spacing-big;
    }
  }
}
</style>
