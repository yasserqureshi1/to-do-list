<template>
	<ion-page>
		<ion-header :translucent="true">
			<ion-toolbar>
				<ion-title>To-Do List</ion-title>
			</ion-toolbar>
		</ion-header>
		
		<ion-content :fullscreen="true">
		<ion-header collapse="condense">
			<ion-toolbar>
				<ion-title size="large">To-Do List</ion-title>
			</ion-toolbar>
		</ion-header>
		
		<div id="container">
			<div v-for="item in items" :key="item">
				<ion-item-sliding>
					<ion-item>
						<ion-label>
							{{ item }}
						</ion-label>
					</ion-item>
					<ion-item-options>
						<ion-item-option color="danger" @click="deleteItem(item)">
							<ion-icon :icon="archive"></ion-icon>
							Delete
						</ion-item-option>
					</ion-item-options>
				</ion-item-sliding>
			</div>
		</div>
		</ion-content>
		<ion-button size="large" style="margin: 20px" @click="openModal">Add item</ion-button>
	</ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton } from '@ionic/vue';
import { defineComponent } from 'vue';
import { IonIcon, IonItem, IonItemOption, IonItemOptions, IonItemSliding, IonLabel, modalController } from '@ionic/vue';
import { archive, ellipsisHorizontal, ellipsisVertical, heart, star, trash } from 'ionicons/icons';
import CreateItem from '../components/CreateItem.vue'
import data from './items.js'

export default defineComponent({
	name: 'Home',
	components: {
		IonContent,
		IonHeader,
		IonPage,
		IonTitle,
		IonToolbar,
		IonButton,
		IonIcon, 
		IonItem, 
		IonItemOption, 
		IonItemOptions, 
		IonItemSliding, 
		IonLabel, 
	},
	setup() {
		return {
			archive, 
			ellipsisHorizontal, 
			ellipsisVertical,
			heart, 
			star, 
			trash
		}
	},
	data: function() {
		return {
			items: data
		}
	},
	methods: {
		async openModal() {
			const modal = await modalController
				.create({
					component: CreateItem,
					cssClass: 'my-custom-class',
					componentProps: {
						title: 'New Title'
					},
				})
			return modal.present();
		},
		deleteItem(item) {
			console.log(item)
			const index = this.items.indexOf(item);
			if (index > -1) {
				this.items.splice(index, 1);
			}
		}
	},
});
</script>

<style scoped>
#container {
  position: absolute;
  left: 0;
  right: 0;

}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>