<template>
  <div>
    <header-bar></header-bar>
    <alerts :alerts="alerts"></alerts>
    <router-view></router-view>
  </div>
</template>

<script>
import Notes from './components/notes/Index'
import UpdateModal from './components/notes/UpdateModal'
import CreateNoteForm from './components/notes/Create'
import Alerts from './components/Alerts'
import EventBus from './components/EventBus'
import HeaderBar from './components/HeaderBar'

export default {
  name: 'app',
  components: {
    Notes,
    CreateNoteForm,
    UpdateModal,
    HeaderBar,
    Alerts
  },
  data () {
    return {
      alerts: []
    }
  },
  created () {
    EventBus.$on('alert', this.showAlert)
  },
  beforeDestroy () {
    EventBus.$off('alert')
  },
  methods: {
    showAlert (alert) {
      this.alerts.push(alert)
      setTimeout(() => {
        this.alerts.splice(alert, 1)
      }, alert.duration || 1500)
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Josefin+Sans');
  *{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  html{
    font-family: 'Josefin Sans', sans-serif;
  }
  body{
    background: #FAFAFA;
    padding: 0 1rem;
  }
  textarea, input, button { outline: none; }
</style>
