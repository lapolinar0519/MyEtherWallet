<template>
  <div class="mew-component--accordion-menu-container user-select--none">
    <div v-for="(mainItems, mainKey) in menuItems" :key="mainKey">
      <!-- Main menus -->
      <div
        :ref="getMenuRef(mainItems.url)"
        class="cursor--pointer"
        @click="routerPush(mainItems.url)"
      >
        <div class="d-flex align-center">
          <img
            class="dark mr-3"
            width="26"
            height="26"
            :src="mainItems.iconDark"
          />
          <img
            class="light mr-3"
            width="23"
            height="23"
            :src="mainItems.iconLight"
          />
          <div class="white--text">{{ mainItems.name }}</div>
        </div>
        <!-- Sub menus -->
        <div v-for="(subItems, subKey) in mainItems.children" :key="subKey">
          <div
            :ref="getMenuRef(subItems.url)"
            class="submenu white--text cursor--pointer"
            @click="
              routerPush(subItems.url, getMenuRef('parent' + mainItems.url))
            "
          >
            {{ subItems.name }}
          </div>
        </div>
      </div>
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
          url: '/wallet/send/sendtx',
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
          url: '/wallet/contract/interact',
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
  computed: {},
  watch: {
    /*
    $route(to, from) {
      console.log(to);
      console.log(from);
    }
    */
  },
  created() {
    this.currentURL = this.$route.path;
    console.log(this.$refs);
  },
  methods: {
    getMenuRef(url) {
      if (url) {
        return url.replace(/[^\w\s]/gi, '_');
      }
      return 'aaa';

      //return sourceString.replace('/', '');
    },
    routerPush(url) {
      this.currentURL = url;
      this.$router.push({ path: url }, () => {});
    }
  }
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles/GlobalVariables.scss';
.main-item,
.sub-item {
  color: white;
}
</style>
