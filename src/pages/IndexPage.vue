<template>
  <q-page class="column items-center">
    <div class="row items-center main_header" style="z-index: 5">
      <q-btn
        flat
        no-caps
        color="#00000080"
        class="text_button"
        :class="{
          text_button_active: currentView === 'WalletView',
        }"
        label="Wallet"
        @click="currentView = 'WalletView'"
      />
      <q-btn
        flat
        no-caps
        color="#00000080"
        class="text_button"
        :class="{
          text_button_active: currentView === 'DonorView',
        }"
        label="Become a donor"
        @click="currentView = 'DonorView'"
      />
    </div>
    <div
      class="column items-center"
      style="width: 100vw; height: 100vh; z-index: 3"
    >
      <WalletView
        v-if="currentView === 'WalletView'"
        :provider="provider"
        :signer="signer"
        :contract="contract"
        :contract_signer="contract_signer"
        :contract_address="contract_address"
        :address="address"
        @connect_wallet="connectWallet()"
      />
      <DonorView v-if="currentView === 'DonorView'" />
    </div>
  </q-page>
</template>

<script>
import { ethers } from "ethers";
import WalletView from "../components/WalletView.vue";
import DonorView from "../components/DonorView.vue";

export default {
  name: "IndexPage",
  components: {
    WalletView,
    DonorView,
  },
  data() {
    return {
      provider: null,
      signer: null,
      address: null,
      currentView: "WalletView",
      contract_address: "0x4628D7A10CD9B44339822Bc99f2A4e578D28BDDb",
      contract_signer: null,
      contract: null,
      abi: [
        "function withdraw(uint256 amount) public",
        "function repay(uint256 amount) public",
        "function hasParticipant(address user) public view returns(bool)",
        "function amountAvailable(address user) public view returns(uint256)",
        "event UserHasBeenAdded(address user)",
      ],
    };
  },
  async mounted() {
    this.provider = new ethers.providers.Web3Provider(window.ethereum);
    await this.setAccountDetails();
  },
  methods: {
    async connectWallet() {
      await this.provider.send("eth_requestAccounts", []);
      await this.setAccountDetails();
    },
    async setAccountDetails() {
      try {
        this.signer = await this.provider.getSigner();
        this.address = await this.signer.getAddress();
        this.contract = new ethers.Contract(
          this.contract_address,
          this.abi,
          this.signer
        );
        this.contract_signer = await this.contract.connect(this.signer);
      } catch (e) {
        this.signer = null;
        this.address = null;
        this.contract = null;
        this.contract_signer = null;
      }
    },
  },
};
</script>

<style lang="scss">
@media only screen and (min-width: 1365px) {
  .main_header {
    position: absolute;
    top: 0;
    width: 1366px;
    height: 140px;
    max-width: 100%;
    padding: 0 16px;
  }

  .text_button {
    font-weight: 700;
    font-size: 28px;
    line-height: 33px;
    border-radius: 18px;
    margin-right: 12px;

    .q-btn__content {
      color: #00000080;
    }

    &.text_button_active {
      .q-btn__content {
        color: #000000;
      }
    }
  }
}

@media only screen and (max-width: 1366px) {
  .main_header {
    position: absolute;
    top: 0;
    width: 100vw;
    height: 10.248902vw;
    max-width: 100%;
    padding: 0 1.171303vw;
  }

  .text_button {
    background: #f5f5f5ea;
    font-weight: 700;
    font-size: 2.04978vw;
    line-height: 2.415813vw;
    border-radius: 1.317716vw;
    margin-right: 0.878477vw;

    .q-btn__content {
      color: #00000080;
    }

    &.text_button_active {
      .q-btn__content {
        color: #000000;
      }
    }
  }
}
</style>
