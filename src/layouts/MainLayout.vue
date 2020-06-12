<template>


  <div id="q-app" ref="home">
    <div>
<!--      <q-toolbar class="col-8 bg-grey-3">
      <q-toolbar-title class="a">{{$t('hello')}} freeosfreeos (TEST WEBSITE)</q-toolbar-title>
      <q-select
        label="Select"
        v-model="lang"
        map-options
        :options="langs"
        />
      </q-toolbar>
-->
      <!-- <q-toolbar class="col-4 bg-primary text-white"> -->

        <q-toolbar class="bg-primary text-white">

            <!-- <div class="col-xs-12 col-lg-3 "> -->
              <div> <img src="../assets/unnamed.png" width="50px" alt=""/>
              </div>
              <q-space />

             <div v-if="!state.accountInfo && !mobileWallet">
               <q-btn color="primary" label="LOGIN">
               <q-menu
                  transition-show="jump-down"
                  transition-hide="jump-up"
                  >
                  <q-list style="min-width: 100px">
                   <q-item clickable>
                       <div @click="connectWallet('scatter')">scatter</div>
                   </q-item>
                   <q-item clickable>
                       <div style="padding-top:15px;" @click="connectWallet('ledger')">ledger</div>
                   </q-item>
                   </q-list>
               </q-menu>
               </q-btn>
             </div>

             <q-btn flat style="color: #00BFFF"  @click="goto('rules')" label="Rules" ></q-btn>
             <q-btn flat style="color: #00BFFF" @click="goto('what')" label="What is FREEOS?" ></q-btn>
             <q-btn icon="settings" round color="#00BFFF" @click="layout = true" ></q-btn>

        </q-toolbar>
      <!-- </q-toolbar> -->

      <div class="text-center q-pa-md q-gutter-sm; padding: 24px;">
        <p class="bottom-three"></p>
        <img src="../assets/download.png" class="rounded mx-auto d-block margin-top:37px;" alt="..." width="15%" height="15%">
        <h5 class="h5-responsive text-white">{{$t('motto')}}</h5>
        <div v-if="active">
        <q-btn
          :loading="loading2"
          :percentage="percentage2"
          size="lg"
          outline rounded
          style="color: #00BFFF"
          @click="startComputing(2)"
          label="CLAIM FREEOS" >
        </q-btn></div>
        <div v-else>
          <q-btn
            size="lg"
            outline rounded
            style="color: #00BFFF"
            disable
            label="CLAIM FREEOS" >
          </q-btn>
        </div>
      </div>

      <div v-if="state.accountInfo" class="text-center q-pa-md q-gutter-sm; padding: 24px;">
      <q-btn color="indigo" v-on:click="logout()" >
        <div class="row items-center no-wrap">
          <q-icon left name="close"></q-icon>
          <div class="text-center">
            Welcome {{ wallet.accountInfo.account_name }} <br>
            Balance: {{ state.accountInfo.core_liquid_balance }}
          </div>
        </div>
      </q-btn>
      </div>

    <div id="q-app">
      <div class="flex flex-center column">
        <div id="parent" class="full-width row wrap justify-center items-baseline content-center" style="overflow: hidden; padding: 24px;">
          <div class="col-9 q-col-gutter-x-xl div-with-bg" style="overflow: auto;">
            <q-card class="div-with-bg">
              <q-card-section>
                <h5>Air Claim Rules</h5>
                <p style="font-size:18px;">{{$t('rules1')}}</p>
                <p style="font-size:18px;">{{$t('rules2')}}</p>
                <p style="font-size:18px;">{{$t('rules3')}}</p>
                <p>{{data1}}  </p>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </div>



      <q-card-section>
        <div class="q-pa-md">
          <q-table
            dense
            :data = "data1"
            :columns="columns"
            row-key="name"
            color="amber"
          ></q-table>
        </div>
      </q-card-section>


<div class="flex flex-center column">
        <div id="parent" class="full-width row wrap justify-center items-baseline content-center" style="overflow: hidden; padding: 24px;">
          <div class="col-9 q-col-gutter-x-xl div-with-bg" style="overflow: auto;">

<q-list class="col-9 q-col-gutter-x-xl div-with-bg" style="overflow: auto;">
        <h5 class="text-center">What is FREEOS?</h5>
        <q-expansion-item style="font-size:20px;"
          switch-toggle-side
          expand-separator
          label="A Citizenship into a Free and Democratic Economy"
        >
          <q-card class="div-with-bg">
            <q-card-section class="">
              <p style="font-size:18px;">{{$t('comment1')}}</p>
              <p style="font-size:18px;">{{$t('comment2')}}</p>
              <p style="font-size:18px;">{{$t('comment3')}}</p>
            </q-card-section>
          </q-card>
        </q-expansion-item>
        <q-expansion-item style="font-size:20px;"
          switch-toggle-side
          expand-separator
          label="A Responsible Universal Basic Income (UBI) that is not merely a
          hand-out"
        >
          <q-card class="div-with-bg">
            <q-card-section>
               <p style="font-size:18px;">{{$t('comment4')}}</p>

              <p class="font-size:18px;">FREEOS is a grand experiment in whether the levers and control of an
              economy can be handed over to the people, with some mathematical-based
              constraints and safety measures—to provide the tools for responsible,
              economic self-management <i>en masse</i>. It is the belief that people will
              come together to help themselves and each other if the right tools are
                given to help guide and empower such decisions.</p>
            </q-card-section>
          </q-card>
        </q-expansion-item>

        <q-expansion-item style="font-size:20px;"
          switch-toggle-side
          expand-separator
          label="FREEOS is Freedom—for All of Us"
        >
          <q-card class="div-with-bg">
            <q-card-section>
              <p>FREEOS is not simply freedom for freedom’s sake. It is not merely a
                rallying cry. It does not just represent “freedom from”. Instead, it
                represents “freedom for”. Freedom for determining the economic well-being
                for oneself and for the greater global community that we all live within.</p>
            </q-card-section>
          </q-card>

        </q-expansion-item>
      </q-list>

          </div>
        </div>
      </div>










      <div class="q-pa-md" style="max-width: 85%" ref="what">

      </div>

      <div class="text-center">
        <h6 class="h6-responsive text-white">For more information on FREEOS, go to: <a href="http://freeos.io">freeos.io</a></h6>
        <q-btn flat dense size="12px" style="color: #00BFFF"  @click="goto('home')" label="Home" ></q-btn>
        <q-btn flat dense style="color: #00BFFF" size="12px" @click="goto('rules')" label="Claim Rules" ></q-btn>
        <q-btn flat dense style="color: #00BFFF" size="12px" @click="goto('what')" label="What is FREEOS?" ></q-btn>
      </div>
      <div class="text-center q-pa-md q-gutter-sm">
        <q-btn round size="sm" color="blue" icon="ion-logo-twitter"></q-btn>
        <q-btn round size="sm" color="blue" icon="ion-logo-github"></q-btn>
        <q-btn round size="sm" color="blue" icon="ion-logo-reddit"></q-btn>
        <q-btn round size="sm" color="blue" icon="ion-logo-linkedin"></q-btn>
        <q-btn round size="sm" color="blue" icon="ion-paper-plane"></q-btn>
      </div>



      <q-dialog v-model="layout" persistent>
        <q-layout view="Lhh lpR fff" container class="bg-white">
          <q-header class="bg-primary">
            <q-toolbar>
              <q-btn flat @click="drawer = !drawer" round dense icon="menu" ></q-btn>
              <q-toolbar-title>Header</q-toolbar-title>
              <q-btn flat v-close-popup round dense icon="close" ></q-btn>
            </q-toolbar>
          </q-header>

          <q-footer class="bg-black text-white">
            <q-toolbar inset>
              <q-toolbar-title>Only for Development.</q-toolbar-title>
            </q-toolbar>
          </q-footer>

          <q-drawer bordered v-model="drawer" :width="200" :breakpoint="600" content-class="bg-grey-3 q-pa-sm">
            <q-list dark>
              <q-item-label header class="text-blue-5">Navigation</q-item-label>

              <q-item
                v-for="nav in navs"
                :key="nav.label"
                :to="nav.to"
                class="text-blue-5"
                exact
                clickable>
                <q-item-section avatar>
                  <q-icon :name="nav.icon" />
                </q-item-section>
                <q-item-section>
                  <q-item-label>{{ nav.label }}</q-item-label>
                </q-item-section>
              </q-item>

            </q-list>

          </q-drawer>

          <q-page-container>
            <q-page padding>
            <router-view />
            </q-page>
          </q-page-container>
        </q-layout>
      </q-dialog>




    </div>
    </div>



</template>

<script>  //Version 10 th July
import { initAccessContext } from "eos-transit";
import scatter from "eos-transit-scatter-provider";
import ledger from "eos-transit-ledger-provider";
import lynx from "eos-transit-lynx-provider";
import tp from 'eos-transit-tokenpocket-provider';
import meetone from 'eos-transit-meetone-provider';
//import { setTimeout } from 'timers';


  import { openURL } from "quasar";
  import axios from "axios";
  import { mapGetters } from "vuex";
  import data1 from './datatab.json';
  //import { Notify } from 'quasar';

  export default {
  name: 'MyLayout',
  data () {
    return {
      active: true, //Claim Active?
      nav: navigator.userAgent,
      mobileWallet: false,
      accountsModal: false,
      finishedVoting: false,
      message: {},
      accessContext: null,
      wallet: null,
      state:{},
      walletId: "scatter",
      discoveryData: [],

      email_address: "",
      language: "",
      onsubscribemsg: "",
      loading: false,
      langs: [
    {
    label: 'German',
    value: 'de'
    },
    {
    label: 'US English',
    value: 'en-us'
    }
    ],
lang: this.$i18n.locale,
      leftDrawerOpen: this.$q.platform.is.desktop,
      loading2: false,
      percentage2: 0,
      interval1: 0,
      interval2: 0,
      layout: false,

      moreContent: true,
      drawer: false,
      navs: [
        {
          label: 'API',
          icon: 'list',
          to: '/api'
        },
        {
          label: 'Settings',
          icon: 'settings',
          to: '/settings'
        }
      ],


      columns: [  //need to be rewritten for the correct table, also verify json format of the data table TODO
        {
          name: 'id',
          required: true,
          label: 'Week',
          align: 'left',
          field: 'id'
        },
        { name: 'email', align: 'center', label: 'HODL Requirement', field: 'email' },  //actually wrong TODO
        { name: 'first_name', label: 'Reward', field: 'first_name' }
      ],
      data1: []
    }},

  created() {
    //if client is using mobile wallet (Now set for Lynx)
    if (navigator.userAgent.toLowerCase().includes('eoslynx')){
      this.mobileWallet = true;
      this.walletId = 'EOS Lynx';
      //if lynxMobile is already loaded, initialize transit
      if (window.lynxMobile) this.initTransit();
      //otherwise wait for lynxMobile to load first
      else window.addEventListener("lynxMobileLoaded", ()=> this.initTransit());
    }
    else if (navigator.userAgent.toLowerCase().includes('tokenpocket')){
      this.mobileWallet = true;
      this.walletId = 'TokenPocket';
      //if TokenPocket is already loaded, initialize transit
      if (window.scatter) this.initTransit();
      //otherwise wait for TokenPocket to load
      else window.addEventListener("scatterLoaded", ()=> this.initTransit());
    }
    else if (navigator.userAgent.toLowerCase().includes('meet.one')){
      this.mobileWallet = true;
      this.walletId = 'meetone_provider';
      // initialize transit with Meet.One wallet (transit will wait for window.scatter to load)
      this.initTransit();
    }
    //if client is not using a mobile wallet
    else this.initTransit();
  },

  watch: {
    lang(lang) {
      this.$i18n.locale = lang.value
      // set quasar's language too!!
      import(`quasar/lang/${lang.value}`).then(language => {
        this.$q.lang.set(language.default)
      })
    },
    state(val){
      //watching state variable to provide custom notifications to user
      if(!val.connecting && this.message.connecting && this.walletId!=='ledger')
        this.message.connecting = false;
      if(this.message.authenticating)
        this.message.authenticating = false;
      if (val.connecting)
        {this.message.connecting = true;
          this.$q.notify({message: 'Connecting: Connecting to ${this.walletId}', type:'info', duration: 3000});
        }
      else if (val.authenticating)
        {this.message.authenticating = true;
          this.$q.notify({message: 'Authenticating: Logging in to ${this.walletId}', type: 'info', duration: 3000});
        }
      else if (val.authenticationError)
        this.$q.notify({message: 'Authentication Error: ${val.authenticationErrorMessage}', type:'negative', duration: 5000,});
      else if (val.connectionError)
        this.$q.notify.error({message: 'Connection Error": ${val.connectionErrorMessage}', type:'negative', duration: 5000});
      else if(val.accountInfo){
        if( this.message.accountInfo) this.message.accountInfo = false;
        this.message.accountInfo = true; this.$q.notify({message: 'Success: Logged in successfully as ${val.accountInfo.account_name}', type:'positive', duration: 3000});
        this.accountsModal = false;
        //once user logs in successfully with scatter, save variable to localstorage to allow auto login
        localStorage.autoLogin = this.walletId;
      }
    }
  },

  computed: {
    //reactive accounts list of all discovered public keys
    accounts() {
      var list = [];
      if (this.discoveryData.keyToAccountMap)
        for (var key of this.discoveryData.keyToAccountMap)
          if (key.accounts && key.accounts[0])
            list.push(key);
      return list;
    },
    progress(){return this.state.connecting || this.state.authenticating || this.state.fetchingAccount || false}
  },

  mounted() {
    //this.loading = true;
      //  axios.get("datatab.json").then(response => (this.data1 = response.data));
    axios
      .get('../statics/rawdata.json')
      .then(response => (this.data1 = response.data.data))
      .catch(error => console.log(error))
    //  .finally(() => this.loading = false)
    console.log('*** data table loaded ... ***')
  },

  methods: {
    goto(refName) {
      let element = this.$refs[refName];
      console.log(element);
      let top = element.offsetTop;
      window.scrollTo(0, top);
    },

initTransit(){
      var options = {

		  appName: "quizinfo1234",
          network: {
          blockchain:'eos',
          protocol:'https',
          host:'api-kylin.eosasia.one',
          port:443,
          chainId:'5fff1dae8dc8e2fc4d5b23b2c7665c97f9e9d8edf2b6485a86ba311c25639191'
        }
      }
      //set desired wallet providers
      if (this.mobileWallet) options.walletProviders = [lynx(), tp(), meetone()];
      else options.walletProviders = [scatter(), ledger()];

      //initialize Transit with the options object
      this.accessContext = initAccessContext(options);

      //Auto connect and login if user is on a mobile wallet
      if (this.mobileWallet) this.connectWallet(this.walletId);

      //auto login to last wallet if user never logged out
      else if (localStorage.autoLogin) this.connectWallet(localStorage.autoLogin);

    },

    async discoverMore(n) {
      for (var i=1;i<n;i++)
        this.discoveryData = await this.wallet.discover({pathIndexList: [i]});
    },

    connectWallet(walletId) {
      this.walletId = walletId;

      //fetch provider using the walletId;
      let provider = this.accessContext.getWalletProviders().find(r=>{return r.id===walletId;});
      if (!provider) return;

      // initialize Transit wallet instance with your desired signature provider
      this.wallet = this.accessContext.initWallet(provider);

      // Subscribe to Transit wallet changes and bind it to a vue variable
      this.wallet.subscribe(walletState =>this.state = walletState);

      this.startLogin(walletId);
    },


    async startLogin() {
      //Connect to wallet provider
      await this.wallet.connect();

      try{
        //start public key discovery for first index
        this.discoveryData = await this.wallet.discover({pathIndexList: [0]});

        //if wallet does not provide public keys (eg. scatter), proceed to login
        if (this.discoveryData.keyToAccountMap.length === 0)
          await this.wallet.login();

        //if wallet provides one or more public keys (eg. ledger), allow user to choose desired account
        else {
          this.accountsModal = true;
          this.message.connecting = 'false'; // needed ??
          this.message.authenticating = 'true'; // needed ??
            this.$q.notify({ message: 'Authenticating: Choose account on ${this.walletId}', type: 'info', duration: 0
          });
          //start async discovery on additional indices
          await this.discoverMore(10);
        }
      }catch(ex){
        this.message.connecting = 'false'; //needed?
        if (this.walletId === 'ledger')
          this.$q.notify({ message: 'Cannot connect to Ledger', type: 'negative' ,duration: 5000
          });
      }
    },

    async accountLogin(index=0, accountIndex=0) {
      let keyObj = this.discoveryData.keyToAccountMap[index];
      await this.wallet.login(keyObj.accounts[accountIndex].account, keyObj.accounts[accountIndex].authorization);
      this.message.authenticating = 'false'; // needed ??
    },

    async logout() {
      //null autologin
      localStorage.removeItem('autoLogin');
      this.$q.notify({ message: "Logging out", type:'info', duration: 0});
      await this.wallet.terminate();
      this.$q.notify({ message: "You have logged out successfully", type:'positive', duration: 3000
      });
    },

    ///openURL,

    changeLang( lang ){
      this.$i18n.locale = lang
    },

    startComputing (id) {
      this[`loading${id}`] = true
      this[`percentage${id}`] = 0
      this[`interval${id}`] = setInterval(() => {
        this[`percentage${id}`] += Math.floor(Math.random() * 8 + 10)
        if (this[`percentage${id}`] >= 100) {
          clearInterval(this[`interval${id}`])
          this[`loading${id}`] = false
          this.showNotif()
        }
      }, 700)

    },

    showNotif () {
      this.$q.notify({
        message: 'You are boiled',
        color: 'teal'
      })
      this.active = false
    },

    beforeDestroy () {
      clearInterval(this.interval1)
      clearInterval(this.interval2)
    }
  }
}
</script>



<style>

#site-container {
    margin: 0px auto;
    text-align: left;
    width: 700px;
    zoom: 1;
    position: relative;
}

  @font-face {
    font-family: 'MyWebFont';
    src: url('../assets/Franklin Gothic Medium Regular/Franklin Gothic Medium Regular.ttf')  format('truetype');
  }
  .my-font {
    font-family:'MyWebFont'
  }

  .bottom-three {
     margin-bottom: 1cm;
  }

  ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: #4080b8;
  }

  li {

    float: left;
  }

  div.a {
    font-size: 12px;
  }

  li a {
    display: block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    float: right;
  }

  li a:hover {
    background-color: #3ab2c9;
  }

  li a:hover:not(.active) {
    background-color: #3ab2c0;
  }

  .div-with-bg {
    background-image: url("../assets/SkyColor.jpg");
    background-size: cover;
    height: 100%;
    width: 100%;
  }

  .text-area {
    font-size: 1.3em;
    margin: 25px;
  }

  body{
    background-image: url("../assets/BetweenNightandDay.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    margin: 0;
    padding: 0;
    height: 100%;
    width: 100%;
  }

  #content {
    width: 990px;
    margin-left: 127px;
    margin-right: 127px;
  }
</style>
