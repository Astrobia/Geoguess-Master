<template>
  <div>
    <div id="section-top">
      <img
        id="background-image" 
        src="@/assets/background.jpg">
      <Header v-if="viewport.width > 450" />
      <HeaderMobile v-else />
      <DialogRoom 
        :dialogRoom="state.dialogRoom"
        @closeDialog="closeDialog" 
      />
      <v-container fluid>
        <v-row
          class="record-wrapper" 
          justify="center">
          <span id="record">Record: {{ record }} km</span>
        </v-row>
        <v-row 
          class="button-wrapper"
          justify="center">
          <button 
            id="single-player-button"
            class="ml-8 mr-8"
            @click="$router.push('street-view')"
          >
            Single Player
          </button>
          <button 
            id="with-friends-button"
            class="ml-8 mr-8"
            @click="state.dialogRoom = true"
          >
            With Friends
          </button>
        </v-row>
      </v-container>
    </div>
    <div id="section-about">
      <v-container>
        <v-row justify="center">
          <div class="section-header">
            <strong>ABOUT</strong>
          </div>
        </v-row>
        <v-row justify="center">
          <div class="description-wrapper">
            Geoguesser is based on SpiderHand's Gueoguess Master codebase based on Geogessr. Players compete how close each player can guess a random locations in five rounds. You can play multiplayer game with your friends up to five friends. The first player creates a room and decide a room size, and then other players type the same room name name as the first player decided and the game will start. If you start getting inverted colours or black screens the site probably hit it's quota, this should reset daily. Please don't share the site publically.
          </div>
        </v-row>
      </v-container>
    </div>
    <Footer />
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, computed, inject, } from '@vue/composition-api'

import Header from '@/components/widgets/bar/Header.vue'
import HeaderMobile from '@/components/widgets/bar/HeaderMobile.vue'
import Footer from '@/components/widgets/footer/Footer.vue'
import DialogRoom from '@/components/widgets/dialog/DialogRoom.vue'

export default defineComponent({
  components: {
    Header,
    HeaderMobile,
    Footer,
    DialogRoom,
  },

  setup() {
    const viewport = inject('viewport')

    const state = reactive<{
      dialogRoom: boolean;
    }>({
      dialogRoom: false,
    })

    const record = computed<string>(() => {
      return localStorage.getItem('record') !== undefined
              ? localStorage.getItem('record')!
              : ''
    })

    function closeDialog(): void {
      state.dialogRoom = false
    }

    return {
      viewport,
      state,
      record,
      closeDialog,
    }
  }
})
</script>

<style scoped>
button {
  width: 244px;
  height: 44px;
  border: none;
  border-radius: 40px;
  font-size: 14px;
}

#single-player-button {
  background-color: #FF5252;
  color: #FFFFFF;
}

#with-friends-button {
  background-color: #43B581;
  color: #FFFFFF;
}

#section-top {
  position: absolute;
  width: 100%;
  height: 640px;
  left: 0px;
  top: 0px;
  background: linear-gradient(#071D3E, #06121D);
}

#section-top * {
  z-index: 1;
}

#background-image {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0.4;
  z-index: 0 !important;
}

#section-about {
  position: absolute;
  width: 100%;
  height: 430px;
  left: 0px;
  top: 640px;
  background: #FAFAFA;
}

.record-wrapper {
  position: absolute;
  width: 100%;
  top: 225px;
}

.button-wrapper {
  position: absolute;
  width: 100%;
  top: 300px;
}

.section-header {
  position: absolute;
  top: 94px;
}

.description-wrapper {
  position: absolute;
  top: 148px;
  padding: 0 18%;
  color: #777777;
}

#record {
  font-size: 26px;
  font-weight: 700;
  color: #FFFFFF;
}

@media (max-width: 450px) {
  #section-top {
    height: 480px;
  }

  .record-wrapper {
    top: 120px;
  }

  #record {
    font-size: 18px;
  }

  .button-wrapper {
    top: 200px;
  }

  #single-player-button {
    height: 42px;
    margin-bottom: 24px;
  }

  #section-about {
    top: 480px;
    height: 480px;
  }

  .section-header {
    top: 24px;
  }

  .description-wrapper {
    top: 60px;
    padding: 0 12%;
  }
} 
</style>
