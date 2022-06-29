<template>
  <div class="mb-1">
    <Card>Personenbezogene Daten</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div class="flex -m-05">
        <FormulateInput
          type="file"
          name="file"
          label="Foto"
          validation="required|mime:image/jpeg,image/png,image/gif"
          :value="image"
          @change="readImage"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Name"
          validation="required"
          v-model="name"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="E-Mail"
          validation="required"
          v-model="mail"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Nummer"
          validation="required"
          v-model="phone"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Bildung & Geburt"
          validation="required"
          v-model="education"
          class="p-05 w-1/5"
        />
      </div>
      <div class="flex -m-05">
        <FormulateInput
          type="text"
          label="Straße"
          validation="required"
          v-model="street"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Hausnummer"
          validation="required"
          v-model="number"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="PLZ"
          validation="required"
          v-model="postcode"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Stadt"
          validation="required"
          v-model="city"
          class="p-05 w-1/5"
        />
        <FormulateInput
          type="text"
          label="Land"
          v-model="country"
          class="p-05 w-1/5"
        />
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  import { mapFields } from "vuex-map-fields";
  export default {
    computed: {
      ...mapGetters(["image"]),
      ...mapFields([
        "name",
        "street",
        "number",
        "postcode",
        "city",
        "country",
        "mail",
        "phone",
        "education",
      ]),
    },
    methods: {
      ...mapMutations(["setImage"]),
      readImage(event) {
        const reader = new FileReader();
        reader.onload = (data) => {
          this.setImage(data.target.result);
        };
        reader.readAsDataURL(event.target.files[0]);
      },
    },
  };
</script>

<style></style>
