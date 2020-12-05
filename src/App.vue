<template>
  <div id="container">
      <div class="page-header">
          <h1 class="text-center">연락처 관리 어플리케이션</h1>
          <p>(Dynamic Component + EventBus + Axios)</p>
      </div>
      <component :is="currentView" :contact="contactt"></component>
      <contractList :contactlist="contactlist"></contractList>
  </div>
</template>

<script>
import ContactList from './components/ContactList';
import AddContact from './components/AddContact';
import UpdateContact from './components/UpdateContact';
import UpdatePhoto from './components/UpdatePhoto';
import CONF from './components/Config.js';
import eventBus from './eventBus.js';

export default {
    name: 'app',
    components : { ContactList, AddContact, UpdateContact, UpdatePhoto}
}
</script>

<style>

</style>
