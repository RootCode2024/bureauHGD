<template>
  <div class="container">
    <h2 class="text-lg font-bold mb-4">Renseigner le formulaire</h2>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <!-- Type de facture -->
      <div>
        <label for="typeFacture" class="block font-medium">Type de facture :</label>
        <select id="typeFacture" v-model="form.typeFacture" class="border p-2 rounded w-full">
          <option value="proforma">Proforma</option>
          <option value="definitive">Définitive</option>
        </select>
      </div>

      <!-- Client -->
      <div>
        <label for="client" class="block font-medium">Choisir le client :</label>
        <select id="client" v-model="form.client" class="border p-2 rounded w-full">
          <option v-for="client in clients" :key="client" :value="client">{{ client }}</option>
          <option value="new">Créer un nouveau client</option>
        </select>
        <div v-if="form.client === 'new'" class="mt-2">
          <input type="text" placeholder="Nom du nouveau client" v-model="form.newClient.name" class="border p-2 rounded w-full" />
          <input type="text" placeholder="Adresse du nouveau client" v-model="form.newClient.address" class="border p-2 rounded w-full" />
          <input type="text" placeholder="Téléphone du nouveau client" v-model="form.newClient.phone" class="border p-2 rounded w-full" />
          <input type="text" placeholder="ID du nouveau client" v-model="form.newClient.id" class="border p-2 rounded w-full" />
        </div>
      </div>

      <!-- Dates -->
      <div>
        <label for="dateFacturation" class="block font-medium">Date de facturation :</label>
        <input
          id="dateFacturation"
          type="date"
          v-model="form.dateFacturation"
          class="border p-2 rounded w-full"
        />
      </div>
      <div>
        <label for="dateEcheance" class="block font-medium">Date d'échéance :</label>
        <input
          id="dateEcheance"
          type="date"
          v-model="form.dateEcheance"
          class="border p-2 rounded w-full"
        />
      </div>

      <!-- Objet -->
      <div>
        <label for="objet" class="block font-medium">Objet :</label>
        <textarea
          id="objet"
          v-model="form.objet"
          placeholder="Entrez l'objet de la facture"
          class="border p-2 rounded w-full"
        ></textarea>
      </div>

      <!-- Form repeater -->
      <div>
        <h3 class="font-medium">Désignation des éléments :</h3>
        <div v-for="(ligne, index) in form.lignes" :key="index" class="space-y-2 mb-2">
          <div class="flex space-x-2">
            <input
              type="text"
              v-model="ligne.designation"
              placeholder="Désignation"
              class="border p-2 rounded w-1/4"
            />
            <input
              type="text"
              v-model="ligne.mesure"
              placeholder="Mesure"
              class="border p-2 rounded w-1/4"
            />
            <input
              type="number"
              v-model="ligne.quantite"
              placeholder="Quantité"
              class="border p-2 rounded w-1/4"
            />
            <input
              type="number"
              v-model="ligne.prixUnitaire"
              placeholder="Prix unitaire"
              class="border p-2 rounded w-1/4"
            />
          </div>
          <button
            type="button"
            @click="removeLigne(index)"
            class="text-red-500 hover:underline"
          >
            Supprimer
          </button>
        </div>
        <button
          type="button"
          @click="addLigne"
          class="bg-green-500 text-white px-4 py-2 rounded"
        >
          Ajouter une ligne
        </button>
      </div>

      <!-- NB -->
      <div>
        <label for="nb" class="block font-medium">Ajouter un NB :</label>
        <textarea
          id="nb"
          v-model="form.nb"
          placeholder="Ajouter une note ou un commentaire"
          class="border p-2 rounded w-full"
        ></textarea>
      </div>

      <!-- Total en lettres -->
      <div>
        <div class="text-3xl bg-indigo-600 text-white m-5 p-3 flex justify-center">Total : {{ form.totalPrice.toLocaleString('fr-FR', {style: 'currency', currency: 'XOF'}) }}</div>
        <label for="totalLettres" class="block font-medium">Somme totale en lettres :</label>
        <input
          id="totalLettres"
          type="text"
          v-model="form.totalLettres"
          placeholder="Total en lettres"
          class="border p-2 rounded w-full"
        />
      </div>
      <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-gray-600">valider</button>
      <!-- Boutons -->
      <div class="flex space-x-4 mt-4">
        <button type="button" class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-600">
          Aperçu
        </button>
        <button type="button" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
          Imprimer
        </button>
        <button type="button" class="bg-purple-500 text-white px-4 py-2 rounded hover:bg-purple-600">
          Envoyer par mail
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { reactive, watch } from "vue";

const form = reactive({

  typeFacture: "proforma",

  client: "",

  newClient: {
    name : "",
    address : "",
    phone : "",
    id : "",
  },

  dateFacturation: "",

  dateEcheance: "",

  objet: "",

  lignes: [
    { designation: "", mesure: "", quantite: 0, prixUnitaire: 0 },
  ],

  nb: "",

  totalLettres: "",

  totalPrice: 0
});

const clients = ["Client 1", "Client 2", "Client 3"];

function addLigne() {
  form.lignes.push({ designation: "", mesure: "", quantite: 0, prixUnitaire: 0 });
}

function removeLigne(index) {
  form.lignes.splice(index, 1);
}

watch(
  () => form.lignes,
  () => {
    form.totalPrice = form.lignes.reduce((total, line) => total + line.quantite * line.prixUnitaire, 0);
  },
  { deep: true }
);

</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 16px;
  font-family: Arial, sans-serif;
}
</style>

