<template>
  <div v-if="!twitchIsAuthenticated()">
    <TwitchConnectionButton></TwitchConnectionButton>
  </div>
  <div v-else>
    <p>Je suis lààààà</p>
  </div>
</template>

<script setup>
import TwitchConnectionButton from "@/components/TwitchConnectionButton.vue";

let accessToken = undefined;

function getUrlQueryStringParams() {
  const uri = location.hash.slice(1).split("&");
  const params = {};

  for (let i in uri) {
    let key = decodeURIComponent(uri[i].split("=")[0]);
    params[key] = decodeURIComponent(uri[i].split("=")[1]);
  }

  return params;
}
function twitchIsAuthenticated() {
  const params = getUrlQueryStringParams();
  accessToken = params.access_token;

  return params.access_token !== undefined;
}

// TODO: Voir pourquoi quand connexion, le bouton ne part pas

window.addEventListener("load", twitchIsAuthenticated)

</script>

<style scoped>

</style>
