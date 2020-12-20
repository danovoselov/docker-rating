<template>
  <div>
    <h1>Рейтинг</h1>
    <table>
      <thead>
      <tr>
        <th>Ранг</th>
        <th>Командир</th>
        <th>Очки</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index) in list" :key="'item_' + index">
        <td>{{ index + 1 }}</td>
        <td>{{ item[1] }}</td>
        <td>{{ item[2] }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'rating',
  data() {
    return {
      list: [],
    }
  },
  beforeCreate() {
    let url = 'https://sheets.googleapis.com/v4/spreadsheets/1PRBmob6EsmW8QN7qonAQ5GleDcHvVdKodqaZkBv-JxY/values/Рейтинг!A3:C26'
    axios.get(url, {
      params: {
        key: 'AIzaSyATO9dsaG0YUy3F1fGvhx-6An_FFHSD0L0'
      }
    }).then((response) => {
      response.data.values.sort(function (a, b) {
        return b[2] - a[2]
      });
      this.list = response.data.values;
    });
  }
}
</script>
