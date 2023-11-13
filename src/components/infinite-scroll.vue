<template>
  <div>
    <ul ref="listEl">
      <li v-for="(user, index) in userList" :key="index">
        {{ user.firstName }}
      </li>

      <p>Fetching more users... please hold</p>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import getUsers from "../api/getUsers";
import { useInfiniteScroll } from "@vueuse/core";

const listEl = ref(null);

const usersToShow = 15;

const userList = ref(await getUsers(usersToShow, 0));

const fetchingData = ref(null);

const getUsersOnScroll = async () => {
  fetchingData.value = true;
  await new Promise((res) => setTimeout(res, 2000));

  const newUsers = await getUsers(usersToShow, userList.value.length);

  fetchingData.value = null;

  userList.value.push(...newUsers);
};

onMounted(() => {
  useInfiniteScroll(listEl, async () => {
    await getUsersOnScroll();
  });
});
</script>

<style scoped>
ul {
  background-color: #41b480;
  list-style: none;
  max-height: 500px;
  width: 600px;
  overflow-y: scroll;
  padding: 12px 20px;

  box-shadow: 0px 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 /0.1);
}

li {
  padding: 12px 0;
  color: #fff;
  font-size: 18px;
  text-align: left;
}
</style>
