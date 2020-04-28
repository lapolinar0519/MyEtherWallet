<template>
  <div
    ref="menu"
    class="mew-component--accordion-menu-container user-select--none"
  >
    <div v-for="(mainItems, mainKey) in menuItems" :key="mainKey">
      <!-- Main menus ======================================== -->
      <div
        :ref="getMenuRef('main' + mainItems.url)"
        class="main-menu cursor--pointer d-flex align-center"
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
          width="23"
          height="23"
          :src="mainItems.iconLight"
        />
        {{ mainItems.name }}
      </div>

      <!-- Sub menus ======================================== -->
      <div v-if="mainItems.children" class="sub-menu">
        <div
          v-for="(subItems, subKey) in mainItems.children"
          :key="subKey"
          :ref="getMenuRef(subItems.url)"
          class="cursor--pointer"
          @click="routerPush(subItems.url)"
        >
          {{ subItems.name }}
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
  data() {
    return {
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
  watch: {
    $route(to) {
      this.removeActiveClasses();

      const menuItemRef = this.getMenuRef(to.path);

      if (this.$refs[menuItemRef]) {
        this.$refs[menuItemRef][0].classList.add('active');
        this.$refs[menuItemRef][0].parentNode.parentNode.classList.add(
          'active'
        );
      } else {
        this.$refs['main' + menuItemRef][0].parentNode.classList.add('active');
      }
    }
  },
  methods: {
    removeActiveClasses() {
      const allActiveClasses = this.$refs['menu'].querySelectorAll('.active');
      for (let i = 0; i < allActiveClasses.length; i++) {
        allActiveClasses[i].classList.remove('active');
      }
    },
    getMenuRef(url) {
      return url.replace(/[^\w\s]/gi, '_');
    },
    routerPush(url) {
      this.$router.push({ path: url }, () => {});
    }
  }
};
</script>

<style lang="scss" scoped>
@import '@/assets/styles/GlobalVariables.scss';
.main-menu,
.sub-menu {
  color: white;
}

.sub-menu {
  max-height: 0px;
  overflow: hidden;
}

.active .sub-menu {
  max-height: 500px;
}
</style>
