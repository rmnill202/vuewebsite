<template>
  <div>
    <br> <!-- Section title -->
    <h1>Contact</h1>

    <!-- Primary container -->
    <div class="primaryContainer">

      <div class="email"> <!-- E-mail -->
        <h2>E-mail</h2>
        <div v-for="item in contact.emails">
          <a :href="`mailto:${item.address}`">{{item.address}}</a>
        </div>
      </div>

      <div class="phone"> <!-- Phone -->
        <h2>Phone</h2>
        <span>{{contact.phone}}</span>
      </div>

      <div class="links"> <!-- General Links -->
        <h2>Links</h2>
        <div v-for="item in contact.socialMedia">
          <a :href="item.link">{{item.websiteName}}</a>
        </div>
      </div>

    </div>

    <br><v-divider></v-divider>
  </div>
</template>

<script>
  export default {
    name: 'contact',
    props: ['contact'],
    data() {
      return {
      };
    }
  };
</script>

<style>
  @media only screen and (min-width: 560px) {
    .primaryContainer {
      display: grid;
      grid-template-columns: 50% 50%;
      grid-gap: 20px;
      margin-left: 10%;
      margin-right: 10%;
    }
    .email {
      grid-column: 1 / 2;
      grid-row: 1 / 2;
    }
    .phone {
      grid-column: 1 / 2;
      grid-row: 2 / 3;
    }
    .links {
      grid-column: 2 / 3;
      grid-row: 1 / 3;
    }
  }
    @media only screen and (max-width: 559px) {
    .email, .phone, .links {
      padding-top: 15px;
    }
  }
</style>
