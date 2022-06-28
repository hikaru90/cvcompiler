<template>
  <div>
    <div class="mb-3">
      <Columns>
        <template #left>
          <div class="mb-1">
          <Title>Fähigkeiten</Title>
          <Skillset />
          </div>
            <Title>Sprachen</Title>
          <Languageset />
        </template>
        <template #right>
          <Sections />
        </template>
      </Columns>
    </div>
  </div>

</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    computed: {
      ...mapGetters(["street", "number", "postcode", "city", "country", "mail", "phone"]),
    },
  };
</script>

<style></style>
