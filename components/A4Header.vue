<template>
  <div>
    <div class="mb-1_5">
      <div class="">
        <Columns itemAlignment="items-center">
          <template #left>
            <div class="text-base">
              <div>{{ street }} {{ number }}</div>
              <div>{{ postcode }} {{ city }}, {{ country }}</div>
            </div>
          </template>
          <template #right>
            <div class="text-base">
              <div>{{ mail }}</div>
              <div>{{ phone }}</div>
            </div>
          </template>
        </Columns>
      </div>
    </div>

    <div class="mb-05">
      <Columns itemAlignment="items-center">
        <template #left>
          <ProfilePicture class="" />
        </template>
        <template #right>
          <Name />
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
