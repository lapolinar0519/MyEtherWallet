<template>
  <div class="mew-component--accordion-menu-container user-select--none">
    <div v-for="(mainItems, mainKey) in menuItems" :key="mainKey">
      <div
        class="cursor--pointer d-flex align-center"
        @click="routerPush(mainItems.url)"
      >
        <img
          class="dark mr-3"
          width="26"
          height="26"
          :src="mainItems.iconDark"
        />
        <img
          class="light mr-3"
          width="26"
          height="26"
          :src="mainItems.iconLight"
        />
        <div class="menu-name">{{ mainItems.name }}</div>
      </div>

      <v-list-item-content
        v-for="(subItems, subKey) in mainItems.children"
        :key="subKey"
      >
        <div
          class="menu-sub-item cursor--pointer"
          @click="routerPush(subItems.url)"
        >
          {{ subItems.name }}
        </div>
      </v-list-item-content>
    </div>
  </div>
</template>

<script>
import DashboardLight from '@/assets/images/icons/icon-dashboard-enable.png';
import DashboardDark from '@/assets/images/icons/icon-dashboard-disable.png';

import SendLight from '@/assets/images/icons/icon-send-enable.png';
import SendDark from '@/assets/images/icons/icon-send-disable.png';

import SwapLight from '@/assets/images/icons/icon-swap-enable.png';
import SwapDark from '@/assets/images/icons/icon-swap-disable.png';

import DappCenterLight from '@/assets/images/icons/icon-dapp-center-enable.png';
import DappCenterDark from '@/assets/images/icons/icon-dapp-center-disable.svg';

import ContractLight from '@/assets/images/icons/icon-contract-enable.png';
import ContractDark from '@/assets/images/icons/icon-contract-disable.png';

import SignMessageLight from '@/assets/images/icons/icon-message-enable.png';
import SignMessageDark from '@/assets/images/icons/icon-message-disable.png';

export default {
  components: {},
  data() {
    return {
      activeMenu: 3,
      currentURL: '',
      menuItems: [
        {
          name: 'Dashboard',
          iconDark: DashboardDark,
          iconLight: DashboardLight,
          url: '/wallet/dashboard'
        },
        {
          name: 'Send',
          iconDark: SendDark,
          iconLight: SendLight,
          children: [
            {
              name: 'Send Transaction',
              url: '/wallet/send/sendtx'
            },
            {
              name: 'Send Offline',
              url: '/wallet/send/send-offline'
            },
            {
              name: 'NFT Manager',
              url: '/wallet/send/nft-manager'
            }
          ]
        },
        {
          name: 'Swap',
          iconDark: SwapDark,
          iconLight: SwapLight,
          url: '/wallet/swap'
        },
        {
          name: 'Dapps Center',
          iconDark: DappCenterDark,
          iconLight: DappCenterLight,
          url: '/wallet/dapps'
        },
        {
          name: 'Contract',
          iconDark: ContractDark,
          iconLight: ContractLight,
          children: [
            {
              name: 'Interact with contract',
              url: '/wallet/contract/interact'
            },
            {
              name: 'Deploy contract',
              url: '/wallet/contract/deploy'
            }
          ]
        },
        {
          name: 'Sign Message',
          iconDark: SignMessageDark,
          iconLight: SignMessageLight,
          url: '/wallet/sign'
        }
      ]
    };
  },
  watch: {
    $route(to, from) {
      console.log(to);
      console.log(from);
    }
  },
  created() {
    this.currentURL = this.$route.path;
  },
  methods: {
    routerPush(url) {
      this.currentURL = url;
      this.$router.push({ path: url }, () => {});
    }
  }
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles/GlobalVariables.scss';
</style>
