<template>
  <header class="flex h-[53px] w-full items-center justify-center bg-blue-600">
    <p class="text-2xl text-white">To Do List</p>
  </header>
  <div class="flex h-[100px] items-center justify-center">
    <form @submit.prevent="push">
      <input
        type="text"
        class="w-[80vw] rounded-md border-2 border-stone-400 p-2 text-[14px] focus:border-stone-500"
        placeholder="輸入To Do，按下Enter直接更新"
        v-model="input"
      />
    </form>
    <button
      @click="delAll"
      class="absolute right-10 w-[50px] translate-y-10 bg-gray-600 p-1 text-[10px] text-white"
    >
      清除
    </button>
  </div>
  <div class="flex w-screen translate-y-10 flex-col justify-center gap-7">
    <div
      v-for="(i, index) in list"
      :key="index + i"
      class="mx-auto flex w-[75vw] flex-row items-center justify-between rounded-md border-2 border-stone-500 bg-white py-3 px-4"
    >
      <form @submit.prevent="update(i, index)">
        <input
          :id="index"
          autocomplete="off"
          type="text"
          :value="i"
          class="border-2 border-black bg-white py-1 pl-2 outline-none read-only:border-0 read-only:p-0"
          readonly
        />
      </form>

      <div class="flex w-[50px] items-center justify-between">
        <span class="cursor-pointer" @click="fix(index)">
          <i class="fa-solid fa-pen"></i>
        </span>
        <span class="cursor-pointer" @click="del(index)">
          <i class="fa-solid fa-trash"></i>
        </span>
      </div>
    </div>
    <div class="h-10 w-full"></div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const input = ref("");
    const list = ref([]);
    const fixer = ref("");
    const push = function () {
      if (input.value == "") {
        return;
      }
      list.value.unshift(input.value);
      input.value = "";
    };
    const update = function (i, index) {
      const item = document.getElementById(index);
      i = item.value;
      item.blur();
      item.setAttribute("readonly", "readonly");
    };
    const fix = function (index) {
      const item = document.getElementById(index);
      item.removeAttribute("readonly");
      item.focus();
    };
    const del = function (index) {
      list.value.splice(index, 1);
    };
    const delAll = function () {
      list.value = [];
    };
    return { input, list, fixer, push, fix, del, delAll, update };
  },
};
</script>

<style></style>
