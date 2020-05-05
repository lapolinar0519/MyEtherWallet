<template>
  <WhiteSheet>
    <InterfaceWrap title="Send Transaction">
      <InputSearchCoins label="Type" :items="coins" />
    </InterfaceWrap>
  </WhiteSheet>
</template>

<script>
//import Var from '@/common/plugins/variables.js';
import WhiteSheet from '@/web/components/Common/WhiteSheet';
import InterfaceWrap from '@/web/components/InterfaceWraps/InterfaceWrap1';
//import StdButton from '@/web/components/StdButton';
import InputSearchCoins from '@/components/Inputs/InputSearchCoins';

export default {
  components: { WhiteSheet, InterfaceWrap, InputSearchCoins },
  data() {
    return {
      coins: [
        {
          name: 'Ethereum',
          value: 'eth'
        },
        {
          name: 'Bitcoin',
          value: 'btc'
        }
      ]
    };
  }
};
</script>
