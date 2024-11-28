<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>MaskaApp</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <ion-list>
        <ion-item v-for="cat in cats" :key="cat.id">
          <p>{{ cat.nama }}</p>
          <p>
            <ion-button @click="adopsi(cat.id)">
              Adopsi
            </ion-button>
          </p>
          <ion-img class="img-wrapper" :src="cat.file"></ion-img>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">

import { ref } from 'vue';
import {
  alertController, IonImg, IonList, IonItem, IonButtons, IonContent,
  IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar
} from
  '@ionic/vue';
const message = ref<string>('');
const cats = ref<Array<{ id: number; nama: string; file: string }>>([
  { id: 1, nama: 'Cipa', file: 'assets/img/cipa.png' },
  { id: 2, nama: 'Cipo', file: 'assets/img/cipo.png' },
  { id: 3, nama: 'Garfield', file: '/assets/img/garfield.png' },
  { id: 4, nama: 'Leon', file: '/assets/img/leon.png'  },
  { id: 5, nama: 'Haiku', file: '/assets/img/haiku.png'  },
  { id: 6, nama: 'Mio', file: '/assets/img/mio.png'  },
  { id: 7, nama: 'Maska', file: '/assets/img/maska.png'  }
  // Add more cat objects as needed
]);

const handleButtonClick = async () => {
  message.value = 'Sedang diproses...';
  await new Promise(resolve => setTimeout(resolve, 2000)); // Simulasi operasi asinkron
  message.value = 'Selesai!';
};

const adopsi = async (id: number) => {
  const theCat = cats.value.find(cat => cat.id === id);
  const alert = await alertController
    .create({
      header: 'Konfirmasi',
      message: `Anda akan mengadopsi ${theCat?.nama}`,
      buttons: [
        {
          text: 'Batal',
          role: 'cancel',
          cssClass: 'secondary',
          handler: () => {
            console.log(`Memilih batal adopsi ${theCat?.nama}`);
          },
        },
        {
          text: 'Ok',
          handler: () => {
            console.log(`Memilih adopsi ${theCat?.nama}`);
          },
        },
      ],
    });
  return await alert.present();
};
</script>