<template>
  <div class="flex flex-grow justify-between">
    <div class="flex flex-grow -m-05">
      <Input :value="name" @handle="handleInput('name', ...arguments)" class="p-05 w-1/5"
        >Beschreibung</Input
      >
      <Input
        :value="proficiency"
        @handle="handleInput('proficiency', ...arguments)"
        class="p-05 w-1/5"
        >Prozent</Input
      >
      <Input :value="duration" @handle="handleInput('duration', ...arguments)" class="p-05 w-1/5"
        >Dauer</Input
      >
    </div>
    <div class="flex">
      <div
        @click="shiftUp"
        class="mt-1_7 border border-gray-300 rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer mr-05"
      >
      <span class="text-md mb-01">
        ▲
      </span>
      </div>
      <div
        @click="shiftDown"
        class="mt-1_7 border border-gray-300 rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer mr-05"
      >
        <span class="text-md mt-01">
          ▼
        </span>
      </div>
      <div
        @click="handleDelete"
        class="mt-1_7 bg-red rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer text-white"
      >
      <span class="text-md">
        ╳
      </span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      name: {
        type: String,
        required: true,
      },
      proficiency: {
        type: String,
        required: true,
      },
      duration: {
        type: String,
        required: true,
      },
    },

    methods: {
      handleInput(field, payload) {
        this.$emit("reskill", { field: field, payload: payload });
      },
      handleDelete() {
        this.$emit("delete");
      },
      shiftUp() {
        this.$emit("up");
      },
      shiftDown() {
        this.$emit("down");
      },
    },
  };
</script>

<style></style>
