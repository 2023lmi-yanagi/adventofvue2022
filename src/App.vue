<script setup>
// [x]ユーザーのリストを出す
// [x]入力フォームを作る
// [x]入力フォームに入力された文字列でリストをフィルターする
// [x]debounce（絞り込みを遅延させる）処理をフィルターに組み込む
//   -ライブラリを探して、それを使えるよう
//   -自分で作ってみる（サンプルコードを見つけて参考で実践する）（多分こういうこと、多分こういうことなんじゃないか）
// ...dummy Json APIからとってくる

import { ref, computed } from 'vue';
import { debounce } from "debounce";

const keyword = ref ('');
const users = ref([
    {
        id: 1,
        name: '鈴木太郎',
        email: 'suzukitaro@example.com'
    },
    {
        id: 2,
        name: '佐藤二郎',
        email: 'satoujiro@example.com'
    },
    {
        id: 3,
        name: '田中三郎',
        email: 'tanakasaburo@example.com'
    },
    {
        id: 4,
        name: '山本四郎',
        email: 'yamamotoshiro@example.com'
    },
    {
        id: 5,
        name: '高橋五郎',
        email: 'takahashigoro@example.com'
    }
  ]);
  const filteredUsers = ref(() => {
      const filteredUsers = [];

      for (const user of users.value) {
        if (user.name.includes(keyword.value) || user.email.includes(keyword.value)) {
          filteredUsers.push(user);
        }
      }

      return filteredUsers;
    });

window.debouncedFilteredUsers = debounce(filteredUsers, 200);

</script>

<template>
  <div id="app">
    <input type="text" v-model="keyword">
    <table>
        <tr v-for="user in debouncedFilteredUsers" :key="user.id">
            <td v-text="user.id"></td>
            <td v-text="user.name"></td>
            <td v-text="user.email"></td>
        </tr>
    </table>
</div>
</template>

<style scoped>

</style>
