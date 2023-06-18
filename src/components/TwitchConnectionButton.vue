<template>
  <div class="container">
    <h3>Se connecter à votre compte Twitch</h3>
    <div class="button-container">
      <button
          @click.prevent.once="twitchAuthentication"
          class="twitch-connection"
      >
        <img
            :src="twitchIcon"
            width="30"
            height="30"
            alt="Twitch icon"
        >
        Se connecter
      </button>
    </div>
  </div>
</template>

<script>
import twitchIcon from "@/assets/icons/twitch.svg";
  export default {
    name: "TwitchConnectionButton",
    data () {
      return {
        twitchOauthUrl: "https://id.twitch.tv/oauth2/authorize",
        responseType: "token",
        clientID: "dy1uzbqjug41d0y6zqymg168ewk4ym",
        redirectURI: "http://localhost:5173/",
        scopes: [
            "channel:read:subscriptions",
            "channel:read:vips",
            "moderation:read",
            "user:read:follows"
        ],
        state: "c3ab8aa609ea11e793ae92361f002671",
        twitchIcon
      }
    },
    methods: {
      encodedQueryString(params) {
        let items = [];
        for (let key in params) {
          let value = encodeURIComponent(params[key]);
          items.push(`${key}=${value}`);
        }

        return items.join("&");
      },
      twitchAuthentication() {
        const params = {
          response_type: this.responseType,
          client_id: this.clientID,
          redirect_uri: this.redirectURI,
          scope: this.scopes.join(" "),
          state: this.state
        }

        location.href = `${this.twitchOauthUrl}?${this.encodedQueryString(params)}`;
      }
    }
  }
</script>

<style scoped>
.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.button-container {
  display: flex;
  justify-content: center;
}
.twitch-connection {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  background-color: white;
  border: 2px solid #9146FF;
  padding: .5rem;
  cursor: pointer;
  transition: all .3s ease-in-out;
}
.twitch-connection img {
  margin-right: 5px;
}

.twitch-connection:hover {
  transform: scale(0.95);
}
</style>