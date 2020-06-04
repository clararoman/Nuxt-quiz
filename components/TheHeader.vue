<template>
  <div class="header-wrapper">
    <div class="row">
      <div class="logo-wrapper">
        <div class="logo">
          <nuxt-link :to="'/'">
            <img src="@/assets/logga_7.svg" alt />
          </nuxt-link>
        </div>
      </div>
      <!-- <div class="about-wrap">
        <div class="about">
          <div v-b-modal.modal-1 class="about-toggler">About</div>
        </div>
      </div>-->
      <!-- <div class="col-9">
        <div class>
          <b-modal backdrop id="modal-1">
            <TheAbout />
          </b-modal>
        </div>
      </div>-->
    </div>
  </div>
</template>

<script>
import TheAbout from "@/components/TheAbout.vue";
export default {
  components: {
    TheAbout
  },
  props: {
    logo: {
      Type: String
    }
  }
};
</script>

<style lang="scss">
.header-wrapper {
  background-color: #262626;
  height: 80px;
  color: $light;
  font-weight: 700;
  padding: 0 2rem;
  .row {
    margin-right: 0px !important;
    margin-left: 0px !important;
    align-items: center;
  }
  > * {
    height: 80px;
  }
  .logo svg {
    width: auto;
    height: 80px;
    background-size: cover;
  }
  .about {
    height: 80px;
    padding-top: 28px;
    .about-toggler {
      text-align: right;
      outline-color: rgba(0, 0, 0, 0);
      outline-width: 0px;
    }
  }
  .about-modal {
    z-index: 10;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .about-wrap {
    width: 30%;
  }
  .logo-wrapper {
    width: 70%;
  }
}
</style>