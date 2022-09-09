<template>
  <div
    class="row justify-center"
    style="width: 100%; height: 100%; overflow: auto"
  >
    <div v-if="!address" class="background_img">
      <q-img src="~/assets/ukraine.jpeg" />
      <div class="row justify-center opesea_link">
        <q-btn
          unelevated
          class="base_button big_height"
          text-color="grey-10"
          dense
          href="https://opensea.io/assets/ethereum/0x96c74f5dbbab31ef4d9b38cbf99f57b7edae2160/638"
          target="_blank"
        >
          <div class="column items-start">
            <div
              class="row no-wrap items-center justify-between"
              style="width: 100%"
            >
              <div class="text-left">
                Day X – Ukrainians celebrate victory in the war
              </div>
              <q-icon name="fa-solid fa-chevron-right" />
            </div>
            <div class="text-left owner">Owned by <b>SirensGallery</b></div>
          </div>
        </q-btn>
      </div>
    </div>

    <div v-if="!address" class="column justify-center content_layout">
      <div class="column justify-end">
        <div class="big_header">Connect wallet</div>
        <div class="big_description">
          To receive donation funds you need to auth wia diia on Gitcoin
          Passport
        </div>
        <div class="metamask_div">
          <q-btn
            unelevated
            class="base_button metamask_button"
            text-color="grey-10"
            dense
            @click="$emit('connect_wallet')"
          >
            <div class="row items-center justify-between" style="width: 100%">
              <div>
                {{
                  address
                    ? address.slice(0, 6) + "..." + address.slice(-6)
                    : "Login with MetaMask"
                }}
              </div>
              <q-img src="~/assets/metamask.png" />
            </div>
          </q-btn>
        </div>
        <div class="unstopable_domains_div">
          <q-btn
            unelevated
            disable
            class="base_button"
            text-color="grey-10"
            dense
            @click="$emit('connect_wallet')"
          >
            <div class="row items-center justify-between" style="width: 100%">
              <div>Login with WalletConnect</div>
              <q-img src="~/assets/WalletConnect.png" />
            </div>
          </q-btn>
        </div>
        <div class="how_create">
          <q-btn
            unelevated
            class="base_button small_button"
            text-color="grey-10"
            dense
            href="https://metamask.io/faqs/"
            target="_blank"
          >
            <div
              class="row no-wrap items-center justify-between"
              style="width: 100%"
            >
              <div>How to create a ethereum wallet</div>
              <q-icon name="fa-solid fa-chevron-right" />
            </div>
          </q-btn>
        </div>
        <div class="small_header">Donations for Ukraine</div>
        <div class="small_description">
          This donations going directly to the ukrainians. Lorem ipsum dolor sit
          amet, consectetur adipiscing elit. Vitae nulla et gravida ac lorem
          gravida. Habitasse ultrices sit purus sagittis, egestas ut. Bibendum
          nisl mi aliquet id rhoncus, magna tortor proin congue. Tortor fusce
          erat neque neque, cras donec cursus id sollicitudin.
        </div>
      </div>
    </div>

    <div
      v-if="address && !participant"
      class="row justify-center content_layout"
    >
      <q-card style="border-radius: 24px; padding: 24px">
        <q-card-section>
          <q-circular-progress
            indeterminate
            size="250px"
            color="lime"
            class="q-ma-md"
          />
        </q-card-section>
        <q-card-section>
          <div class="big_header">
            Wait until administrator approves your wallet
          </div>
        </q-card-section>
        <q-card-section class="small_header">
          It can take about 2 minutes
        </q-card-section>
        <q-card-section class="small_header">
          <q-btn
            class="base_button small_button"
            label="Refresh"
            @click="hasParticipant(address)"
          />
        </q-card-section>
      </q-card>
    </div>

    <div
      v-if="address && participant"
      class="row justify-center content_layout"
    >
      <div class="column" style="margin-top: 140px">
        <div class="column">
          <div class="big_header">${{ amount_avialiable }}</div>
          <div class="big_description">Available now</div>
        </div>
        <div class="row items-center mt-40">
          <div class="column items-center mr-36">
            <q-btn
              @click="withdraw(amount_to_withdraw)"
              round
              color="#000000"
              text-color="black"
              class="round_button mb-12"
            >
              <svg
                viewBox="0 0 27 28"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M5.59194 14L1.06528 2.36005C0.750609 1.55071 1.53994 0.776048 2.32128 1.05205L2.44528 1.10405L26.4453 13.104C26.6 13.1813 26.7321 13.2975 26.8286 13.4411C26.925 13.5847 26.9826 13.7509 26.9956 13.9234C27.0087 14.0959 26.9767 14.2688 26.9029 14.4253C26.8291 14.5817 26.716 14.7164 26.5746 14.816L26.4453 14.8934L2.44528 26.8934C1.66794 27.2814 0.822609 26.5667 1.02528 25.7627L1.06528 25.636L5.59194 14L1.06528 2.36005L5.59194 14ZM3.86928 4.05338L7.34928 13H16.1853C16.4269 13.0001 16.6604 13.0876 16.8425 13.2464C17.0246 13.4052 17.1431 13.6246 17.1759 13.864L17.1853 14C17.1852 14.2419 17.0975 14.4755 16.9384 14.6577C16.7793 14.8398 16.5596 14.9581 16.3199 14.9907L16.1853 15H7.34661L3.86794 23.9467L23.7626 14L3.86794 4.05338H3.86928Z"
                  fill="#040404"
                />
              </svg>
            </q-btn>
            <div class="smallest_description">Withdraw</div>
          </div>
          <q-input
            type="number"
            outlined
            v-model="amount_to_withdraw"
            label="Enter amount"
          />
        </div>
        <div class="row items-center mt-40">
          <div
            class="column items-center"
            style="margin-left: 18px; margin-right: 52px"
          >
            <q-btn
              @click="repay(amount_to_repay)"
              round
              color="#000000"
              text-color="black"
              class="round_button mb-12"
            >
              <svg
                viewBox="0 0 27 28"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M5.59194 14L1.06528 2.36005C0.750609 1.55071 1.53994 0.776048 2.32128 1.05205L2.44528 1.10405L26.4453 13.104C26.6 13.1813 26.7321 13.2975 26.8286 13.4411C26.925 13.5847 26.9826 13.7509 26.9956 13.9234C27.0087 14.0959 26.9767 14.2688 26.9029 14.4253C26.8291 14.5817 26.716 14.7164 26.5746 14.816L26.4453 14.8934L2.44528 26.8934C1.66794 27.2814 0.822609 26.5667 1.02528 25.7627L1.06528 25.636L5.59194 14L1.06528 2.36005L5.59194 14ZM3.86928 4.05338L7.34928 13H16.1853C16.4269 13.0001 16.6604 13.0876 16.8425 13.2464C17.0246 13.4052 17.1431 13.6246 17.1759 13.864L17.1853 14C17.1852 14.2419 17.0975 14.4755 16.9384 14.6577C16.7793 14.8398 16.5596 14.9581 16.3199 14.9907L16.1853 15H7.34661L3.86794 23.9467L23.7626 14L3.86794 4.05338H3.86928Z"
                  fill="#040404"
                />
              </svg>
            </q-btn>
            <div class="smallest_description">Repay</div>
          </div>
          <q-input
            type="number"
            outlined
            v-model="amount_to_repay"
            label="Enter amount"
          />
        </div>
      </div>
      <div></div>
      <!-- <div class="column">
        <q-btn
          color="primary"
          label="hasParticipant"
          @click="hasParticipant(address)"
        />
        <q-btn
          class="q-mt-md"
          color="primary"
          label="amountAvailable"
          @click="amountAvailable(address)"
        />
        <q-btn
          class="q-mt-md"
          color="primary"
          label="withdraw"
          @click="withdraw(amount_to_withdraw)"
        />
        <q-btn
          class="q-mt-md"
          color="primary"
          label="repay"
          @click="repay(10)"
        />
        <q-btn
          class="q-mt-md"
          color="primary"
          label="approve"
          @click="approve(10)"
        />
      </div> -->
    </div>
  </div>
</template>

<script>
import { ethers } from "ethers";

export default {
  props: {
    address: {
      type: String,
      default: null,
    },
    signer: {
      type: Object,
      default: null,
    },
    contract_signer: {
      type: Object,
      default: null,
    },
    contract: {
      type: Object,
      default: null,
    },
    provider: {
      type: Object,
      default: null,
    },
    contract_address: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      loader: false,
      amount_to_withdraw: 0,
      amount_to_repay: 0,
      amount_avialiable: 0,
      participant: false,
      withdraw_success: false,
      withdraw_amount: 0,
      repay_success: false,
      repay_amount: 0,
    };
  },

  watch: {
    async contract_signer(newValue, oldValue) {
      await this.hasParticipant(this.address);
    },
  },

  methods: {
    async hasParticipant(address) {
      this.loader = true;

      try {
        let txResponse = await this.contract_signer.hasParticipant(address, {
          gasLimit: await this.contract.estimateGas.hasParticipant(address),
        });

        this.participant = txResponse;

        if (!txResponse) {
          this.contract.on("UserHasBeenAdded", (address) => {
            if (address == this.address) {
              this.participant = true;
              this.amountAvailable(address);
            }
          });
        } else {
          this.amountAvailable(address);
        }
      } catch (e) {
        console.log(e);
        this.loader = false;
      }
      this.loader = false;
    },
    async amountAvailable(address) {
      this.loader = true;

      try {
        let txResponse = await this.contract_signer.amountAvailable(address, {
          gasLimit: await this.contract.estimateGas.amountAvailable(address),
        });

        this.amount_avialiable = ethers.BigNumber.from(txResponse).toString();
      } catch (e) {
        console.log(e);
        this.loader = false;
      }
      this.loader = false;
    },
    async withdraw(amount) {
      this.loader = true;

      try {
        await this.approve(amount);
        let txResponse = await this.contract_signer.withdraw(amount, {
          gasLimit: await this.contract.estimateGas.withdraw(amount),
        });

        this.withdraw_success = true;
        this.amount_to_withdraw = null
        this.amountAvailable(this.address);
      } catch (e) {
        console.log(e);
        this.loader = false;
      }
      this.loader = false;
    },
    async repay(amount) {
      try {
        this.loader = true;

        await this.approve(amount);
        let txResponse = await this.contract_signer.repay(amount, {
          gasLimit: await this.contract.estimateGas.repay(amount),
        });

        this.repay_success = true;
        this.amount_to_repay = null
        this.amountAvailable(this.address);
      } catch (e) {
        console.log(e);
        this.loader = false;
      }
      this.loader = false;
    },
    async approve(amount) {
      this.loader = true;
      let approve_contract = new ethers.Contract(
        "0x3181B80A84F17c5C46442861C65ef8DFe7a8d29E",
        [
          "function approve(address spender, uint256 amount) public returns (bool)",
          "function allowance(address owner, address spender) public view returns (uint256)",
        ],
        this.signer
      );

      try {
        let approve_contract_signer = await approve_contract.connect(
          this.signer
        );

        let txResponse = await approve_contract_signer.allowance(
          this.address,
          this.contract_address,
          {
            gasLimit: await approve_contract.estimateGas.allowance(
              this.address,
              this.contract_address
            ),
          }
        );

        if (ethers.BigNumber.from(txResponse).toString() < amount) {
          txResponse = await approve_contract_signer.approve(
            this.contract_address,
            9999999999,
            {
              gasLimit: await approve_contract.estimateGas.approve(
                this.contract_address,
                9999999999
              ),
            }
          );
        }
      } catch (e) {
        console.log(e);
        this.loader = false;
      }
      this.loader = false;
    },
  },
};
</script>

<style lang="scss">
@media only screen and (min-width: 1365px) {
  .background_img {
    position: absolute;
    width: 32%;
    top: 0;
    right: 0;
    bottom: 0;
    .q-img {
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
    }
    .opesea_link {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 30px;
      .q-btn {
        width: 80%;
        height: fit-content !important;
        padding: 12px 16px;
        .q-icon {
          font-size: 20px;
        }
        .owner {
          font-weight: 500;
          font-size: 18px;
          line-height: 21px;
          margin-top: 6px;
        }
      }
    }
  }

  .base_button {
    height: 58px;
    background: #ffffff;
    box-shadow: 0px 4px 24px rgba(0, 0, 0, 0.05) !important;
    border-radius: 16px;
    padding: 0 16px;
    font-weight: 600;
    font-size: 22px;
    line-height: 26px;
    color: #000000 !important;
    text-transform: inherit;

    &.metamask_button {
      background: linear-gradient(92.06deg, #687bdb 15.1%, #6bb2da 88.95%);
      color: #ffffff !important;
    }

    &.small_button {
      font-weight: 500;
      font-size: 20px;
      line-height: 24px;
    }

    &.big_height {
      height: 85px;
    }
  }

  .content_layout {
    width: 1366px;
    max-width: 100%;
    margin-top: 140px;
    margin-bottom: 140px;
    padding: 0 32px;

    .big_header {
      font-weight: 700;
      font-size: 72px;
      line-height: 86px;
    }

    .small_header {
      font-weight: 700;
      font-size: 42px;
      line-height: 50px;
      margin-top: 24px;
    }

    .big_description {
      font-weight: 500;
      font-size: 28px;
      line-height: 33px;
      width: 500px;
      max-width: 70%;
      margin-top: 16px;
    }

    .round_button {
      background: #ffffff;
      width: 60px;
      height: 60px;
      svg {
        width: 27px;
        height: 28px;
      }
    }

    .w-210 {
      width: 210px;
    }

    .mt-40 {
      margin-top: 40px;
    }

    .mr-36 {
      margin-right: 36px;
    }

    .mb-12 {
      margin-bottom: 12px;
    }

    .mt-12 {
      margin-top: 12px;
    }

    .smallest_description {
      font-weight: 500;
      font-size: 24px;
      line-height: 29px;
    }

    .small_description {
      font-weight: 500;
      font-size: 24px;
      line-height: 29px;
      margin-top: 16px;
      width: 757px;
      max-width: 55%;
    }

    .metamask_div {
      margin-top: 48px;
      .base_button {
        width: 358px;
        .q-img {
          width: 44px;
          height: 44px;
        }
      }
    }

    .unstopable_domains_div {
      margin-top: 16px;
      .base_button {
        width: 358px;
        .q-img {
          width: 44px;
          height: 44px;
        }
      }
    }

    .how_create {
      margin-top: 127px;
      .base_button {
        width: 358px;
        .q-icon {
          font-size: 20px;
        }
      }
    }
  }
}

@media only screen and (max-width: 1366px) {
  .background_img {
    position: absolute;
    width: 32%;
    top: 0;
    right: 0;
    bottom: 0;
    .q-img {
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
    }
    .opesea_link {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 2.196193vw;
      .q-btn {
        width: 80%;
        height: fit-content !important;
        padding: 0.878477vw 1.171303vw;
        .q-icon {
          font-size: 1.464129vw;
        }
        .owner {
          font-weight: 500;
          font-size: 1.317716vw;
          line-height: 1.537335vw;
          margin-top: 0.439239vw;
        }
      }
    }
  }

  .base_button {
    height: 4.245974vw;
    background: #ffffff;
    box-shadow: 0vw 0.292826vw 1.756955vw rgba(0, 0, 0, 0.05) !important;
    border-radius: 1.171303vw;
    padding: 0 1.171303vw;
    font-weight: 600;
    font-size: 1.610542vw;
    line-height: 1.903367vw;
    color: #000000 !important;
    text-transform: inherit;

    &.metamask_button {
      background: linear-gradient(92.06deg, #687bdb 15.1%, #6bb2da 88.95%);
      color: #ffffff !important;
    }

    &.small_button {
      font-weight: 500;
      font-size: 1.464129vw;
      line-height: 1.756955vw;
    }

    &.big_height {
      height: 6.222548vw;
    }
  }

  .content_layout {
    width: 100vw;
    max-width: 100%;
    margin-top: 10.248902vw;
    margin-bottom: 10.248902vw;
    padding: 0 2.342606vw;

    .big_header {
      font-weight: 700;
      font-size: 5.270864vw;
      line-height: 6.295754vw;
    }

    .small_header {
      font-weight: 700;
      font-size: 3.074671vw;
      line-height: 3.660322vw;
      margin-top: 1.756955vw;
    }

    .big_description {
      font-weight: 500;
      font-size: 2.04978vw;
      line-height: 2.415813vw;
      width: 36.603221vw;
      max-width: 70%;
      margin-top: 1.171303vw;
    }

    .small_description {
      font-weight: 500;
      font-size: 1.756955vw;
      line-height: 2.122987vw;
      margin-top: 1.171303vw;
      width: 55.417277vw;
      max-width: 55%;
    }

    .metamask_div {
      margin-top: 3.513909vw;
      .base_button {
        width: 26.207906vw;
        .q-img {
          width: 3.221083vw;
          height: 3.221083vw;
        }
      }
    }

    .unstopable_domains_div {
      margin-top: 1.171303vw;
      .base_button {
        width: 26.207906vw;
        .q-img {
          width: 3.221083vw;
          height: 3.221083vw;
        }
      }
    }

    .how_create {
      margin-top: 9.297218vw;
      .base_button {
        width: 26.207906vw;
        .q-icon {
          font-size: 1.464129vw;
        }
      }
    }
  }
}
</style>
