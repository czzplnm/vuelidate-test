<template>
  <ion-page>
    <ion-content>
      <login-form />
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
  import {IonContent, IonPage} from '@ionic/vue';
  import {ellipse, square, triangle} from 'ionicons/icons';
  import LoginForm from "@/components/form/LoginForm.vue";

  export default {
    name: 'LoginPage',
    components: {IonContent, IonPage, LoginForm},
    setup() {
      return {
        ellipse,
        square,
        triangle,
      }
    }
  }
</script>