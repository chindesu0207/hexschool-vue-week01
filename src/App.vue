<script setup>
import { ref } from 'vue'

const menuData = ref([
  {
    id: 1,
    title: '珍珠奶茶',
    desc: '香濃奶茶搭配QQ珍珠',
    price: 50,
    count: 20
  },
  {
    id: 2,
    title: '冬瓜檸檬',
    desc: '清新冬瓜配上新鮮檸檬',
    price: 45,
    count: 18
  },
  {
    id: 3,
    title: '翡翠檸檬',
    desc: '綠茶與檸檬的完美結合',
    price: 55,
    count: 34
  },
  {
    id: 4,
    title: '四季春茶',
    desc: '香醇四季春茶，回甘無比',
    price: 45,
    count: 10
  },
  {
    id: 5,
    title: '阿薩姆奶茶',
    desc: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    count: 25
  },
  {
    id: 6,
    title: '檸檬冰茶',
    desc: '檸檬與冰茶的清新組合',
    price: 45,
    count: 20
  },
  {
    id: 7,
    title: '芒果綠茶',
    desc: '芒果與綠茶的獨特風味',
    price: 55,
    count: 18
  },
  {
    id: 8,
    title: '抹茶拿鐵',
    desc: '抹茶與鮮奶的絕配',
    price: 60,
    count: 20
  }
])

const tempEdit = ref([
  {
    id: '',
    title: '',
    desc: '',
    price: '',
    count: ''
  }
])

const addCount = (product) => {
  const index = menuData.value.findIndex((item) => item.id === product.id)
  menuData.value[index].count++
}

const reduceCount = (product) => {
  const index = menuData.value.findIndex((item) => item.id === product.id)
  menuData.value[index].count--
}

const prepareEdit = (product) => {
  tempEdit.value = { ...product }
}

const confirmEdit = (product) => {
  const index = menuData.value.findIndex((item) => item.id === product.id)
  menuData.value[index]= tempEdit.value
  tempEdit.value = {}
}

const cancelEdit = () => {
  tempEdit.value = {}
}
</script>
<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody v-for="product in menuData" :key="product.id">
      <tr v-if="tempEdit.id === product.id">
        <td><input type="text" v-model="tempEdit.title" /></td>
        <td><input type="text" v-model="tempEdit.desc" /></td>
        <td>{{ product.price }}</td>
        <td>
          <button @click="reduceCount(product)">-</button>{{ product.count
          }}<button @click="addCount(product)">+</button>
        </td>
        <td><button type="button" @click="confirmEdit(product)">修改</button></td>
        <td><button type="button" @click="cancelEdit">取消</button></td>
      </tr>
      <tr v-else>
        <td>{{ product.title }}</td>
        <td>
          <small>{{ product.desc }}</small>
        </td>
        <td>{{ product.price }}</td>
        <td>
          <button @click="reduceCount(product)">-</button>{{ product.count
          }}<button @click="addCount(product)">+</button>
        </td>
        <td><button type="button" @click="prepareEdit(product)">編輯</button></td>
      </tr>
    </tbody>
  </table>
</template>
