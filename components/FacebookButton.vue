<template>
  <div @click="signIn" class="facebook-btn" :class="customClass">
    <img class="icon" src="../assets/facebook_logo.svg" />
    <div class="title">{{ buttonText }}</div>
  </div>
</template>

<script>
export default {
  name: "facebook-button",
  props: {
    customClass: {
      type: String,
      required: false
    },
    buttonText: {
      type: String,
      default: "Sign in with Facebook"
    }
  },  
  methods: {
    async signIn() {
      try {
        const response = await this.$fbAuth.signIn();
        this.$emit('signedIn', response);
      } catch (e) {
        this.$emit('signInError', e);
      }
    }
  }
};
</script>

<style scoped>
.facebook-btn {
  padding: 8px;
  border: thin solid #888;
  border-radius: 5px;
  height: 40px;
  width: 235px;
  display: flex;
  align-items: center;
  cursor: pointer;
  box-shadow: 1px 1px 1px grey;
}

.icon {
  display: block;
  height: 18px;
  width: 18px;
  margin-right: 10px;
}

.title {
  text-transform: uppercase;
  color: #444;
  font-size: 14px;
  font-weight: 500;
  font-family: "Roboto", sans-serif;
}
</style>
