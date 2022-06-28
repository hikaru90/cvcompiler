<template>
  <div class="bg-white px-2 w-full flex h-6 items-center justify-between">
    <div class="flex">
      <FormulateInput
        type="file"
        name="file"
        label="Config"
        validation="mime:text/plain"
        @change="readContent"
        class="mr-1 mb-0"
      />
      <FormulateInput
        type="color"
        name="sample"
        label="Akzentfarbe"
        validation="required"
        v-model="color"
      />
    </div>

    <div>
      <FormulateInput
        type="button"
        label="Config Speichern"
        @click="downloadConfig"
        input-class="shadow-md"
      />
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  import { mapFields } from "vuex-map-fields";
  export default {
    computed: {
      ...mapGetters(["fileContent", "concatenatedFields"]),
      ...mapFields(["color"]),
    },

    methods: {
      ...mapMutations(["setFileContent", "setImage"]),
      readContent(event) {
        const reader = new FileReader();
        reader.onload = (data) => {
          this.setFileContent(data.target.result);
        };
        reader.readAsText(event.target.files[0]);
      },
      downloadConfig() {
        var element = document.createElement("a");
        element.setAttribute(
          "href",
          "data:text/plain;charset=utf-8, " +
            encodeURIComponent(JSON.stringify(this.concatenatedFields))
        );
        element.setAttribute("download", "cvconfig.txt");
        document.body.appendChild(element);
        element.click();
        document.body.removeChild(element);
      },
    },
  };
</script>

<style></style>
