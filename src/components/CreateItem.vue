<template>
    <ion-header>
        <ion-toolbar>
            <ion-title>Create New Item</ion-title>
        </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
        <ion-item>
            <ion-label position="floating">Please type here...</ion-label>
            <ion-input v-model="item"></ion-input>
        </ion-item>
        <div style="text-align: center;">
            <ion-button expand="block" color="primary" @click="save()">Save</ion-button>
            <ion-button expand="block" color="medium" @click="close()">Cancel</ion-button>
        </div>
    </ion-content>
</template>

<script>
import { IonContent, IonHeader, IonTitle, IonToolbar, modalController } from '@ionic/vue';
import { IonLabel, IonInput, IonItem, IonButton } from '@ionic/vue';
import { defineComponent } from 'vue';
import data from '../views/items.js'

export default defineComponent({
    name: 'Modal',
    data() {
        return {
            item: '',
            items: data
        }
    },
    components: { IonContent, IonHeader, IonTitle, IonToolbar,IonLabel, IonInput, IonItem, IonButton },
    methods: {
        save() {
            if (this.item != '') {
                this.items.push(this.item)
            }
            modalController.dismiss();
        },
        close() {
            modalController.dismiss();
        }
    }
});
</script>