<template>
  <div id="editor" class="w-1/2 bg-gray-100 border-r border-gray-200 p-2">
    <EditorPersonendaten />
    <EditorFertigkeiten />
    <EditorLanguages />
    <EditorLeftContent />
    <EditorContent />
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  import { mapFields } from "vuex-map-fields";
  export default {
    computed: {
      ...mapGetters([
        "image",
      ]),
      ...mapFields(["name", "street", "number", "postcode", "city", "country", "mail", "phone", "education"]),
    },
    methods: {
      ...mapMutations([
        "setImage",
      ]),
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
