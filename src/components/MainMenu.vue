<template>
  <div class="main-menu">
    <div>
            <input
          id="fr"
          v-model="language"
          type="radio"
          name="language"
          value="fr"
      >
      <label
          for="fr"
          class="ml-2 mr-2"
      >
        Französich
      </label>
      <input
          id="de"
          v-model="language"
          type="radio"
          name="language"
          value="de"
      >
      <label
          for="de"
          class="ml-2 mr-2"
      >
        Deutsch
      </label>
    <br>
      <input
          id="A"
          v-model="client"
          type="radio"
          name="A"
          value="A"
          @change="applyFilter"
      >
      <label
          for="A"
          class="ml-2 mr-2"
      >
        Kunden A
      </label>
      <input
          id="B"
          v-model="client"
          type="radio"
          name="B"
          value="B"
          @change="applyFilter"
      >
      <label
          for="B"
          class="ml-2 mr-2"
      >
        Kunden B
      </label>
    <br>
    <br>
    <div v-if="isPremium">
      <input
          id="admin"
          v-model="user"
          type="radio"
          name="admin"
          value="admin"
          @change="applyFilterUser"
      >
      <label
          for="admin"
          class="ml-2 mr-2"
      >
        Administrator
      </label>
      <input
          id="user"
          v-model="user"
          type="radio"
          name="user"
          value="user"
          @change="applyFilterUser"
      >
      <label
          for="user"
          class="ml-2 mr-2"
      >
        User
      </label>
    </div>
    </div>
    <h1 align="center">Menü</h1>
    <div align="center">
    <h3>
      <button class="menu-button" @click="analyticsMenu"> 
        {{ analyticsExpanded ? '-' : '+'}} 
      </button> 
      Analytics
    </h3>
    <ul v-if="analyticsExpanded">
      <li>
        <button class="submenu-button" @click="goTo('/dashboard-analytics')"> {{ translate('dashboard') }}</button>
        </li>
      <li>
        <button class="submenu-button" @click="goTo('/reports-analytics')">Reports</button>
      </li>
      <li>
        <button v-bind:class="isAdmin?'submenu-button':'isDisabled'" @click="goTo('/eigne-reports-analytics')">
          Eigene Reports
        </button>
      </li>
      <li>
        <button v-bind:class="isAdmin?'submenu-button':'isDisabled'" @click="goTo('/centricity-analytics')">
          Centricity
        </button>
      </li>
      <li>
        <button v-bind:class="isAdmin?'submenu-button':'isDisabled'" @click="goTo('/plugins-analytics')">
          Plug-Ins
        </button>
      </li>
    </ul>
    <h3>
      <button class="menu-button" @click="crossSellMenu"> 
        {{ crossSellExpanded ? '-' : '+' }}
      </button> 
      Cross Sell
    </h3>
    <ul v-if="crossSellExpanded">
      <li>
        <button  v-bind:class="isPremium?'submenu-button':'isDisabled'" @click="goTo('/dashboard-cross-sell')">
          Dashboard
        </button>
      </li>
      <li>
        <button v-bind:class="isPremium?'submenu-button':'isDisabled'" @click="goTo('/katalog-cross-sell')">
          Katalog
        </button>
      </li>
      <li>
        <button v-bind:class="isPremium?'submenu-button':'isDisabled'" @click="goTo('/widgets-cross-sell')">
          Widgets
        </button>
      </li>
      <li>
        <button v-bind:class="isPremium?'submenu-button':'isDisabled'" @click="goTo('/kampagnen-cross-sell')">
          Kampagnen
        </button>
      </li>
      <li>
        <button  v-bind:class="isPremium?'submenu-button':'isDisabled'" @click="goTo('/reports-cross-sell')">
          Reports
        </button>
      </li>
    </ul>
    
    </div>
    <modal
      v-show="isModalVisible"
      @close="closeModal"
    />
  </div>
  
</template>

<script>
import modal from './Modal.vue';

export default {
  name: 'MainMenu',
  components: {
    modal
  },
  
  data: () => ({
    client: 'A',
    user: 'admin',
    isPremium: true,
    isAdmin: true,
    analyticsExpanded: false,
    crossSellExpanded: false,
    isModalVisible: false,
    language: 'fr',
    translation: {dashboard: 'dashboard-fr'}

  }),
  methods: {
    applyFilter() {
      this.isPremium = (this.client === 'A')
      this.analyticsExpanded = false
      this.crossSellExpanded = false
    },
    applyFilterUser() {
      this.isAdmin = (this.user === 'admin')
    },
    analyticsMenu() {
      this.analyticsExpanded = !this.analyticsExpanded
    },
    crossSellMenu() {
      this.crossSellExpanded = !this.crossSellExpanded
      if (!this.isPremium && this.crossSellExpanded) {
        this.showModal()
      }
    },
    translate(key) {
      if(this.language === 'fr') {
        return this.translation[key]
      } 
      return key            
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    goTo(route) {
      console.log(route)
      window.location = route;
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
.isDisabled {
  border: none;
  cursor: pointer;
  background: transparent;
  color: currentColor;
  cursor: not-allowed;
  opacity: 0.5;
  text-decoration: none;
}
.menu-button {
  border: none;
  font-size: 20px;
  cursor: pointer;
  font-weight: bold;
  color: #0063e4;
  background: transparent;
}
.submenu-button {
  border: none;
  cursor: pointer;
  background: transparent;
}
</style>
