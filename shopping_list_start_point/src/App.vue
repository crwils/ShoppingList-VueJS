<template>
  <body>
    
    <main id="app">
      <div class="unpurchased-container">
        <ul>
          <li
            v-for="(item, index) in items"
            :key="index"
            :class="item.isPurchased ? 'purchased' : 'not-purchased'"
          >
            <span>{{ item.name }}</span>
            <span v-if="item.isPurchased">Purchased ✅ </span>
            <button v-if="!item.isPurchased" v-on:click="buyItem(index)">
              Purchase
            </button>
          </li>
        </ul>
      </div>

      <div class="form-container">
        <form v-on:submit.prevent="saveNewItem">
          <label for="new-item">Add a new item:</label>
          <input type="text" id="new-item" v-model="newItem" />
          <input type="submit" value="Save New Item" />
        </form>
      </div>

      <div class="purchased-container">
        <ul>
          <li
            v-for="(item, index) in purchasedItems"
            :key="index"
            class="purchased-list"
          >
            <span>{{ item.name }}</span>
            <span v-if="item.isPurchased">Purchased ✅</span>
          </li>
        </ul>
      </div>
    </main>

  </body>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          name: "milk",
          isPurchased: false,
        },
        {
          name: "cheese",
          isPurchased: false,
        },
        {
          name: "beans",
          isPurchased: false,
        },
      ],
      newItem: "",
      purchasedItems: []
    };
  },
  methods: {
    saveNewItem: function () {
      if (this.newItem.trim()) {
        this.items.push({
          name: this.newItem,
          isPurchased: false,
        });
        this.newItem = "";
      }
    },
    buyItem: function (index) {
      let item = this.items[index]
      item.isPurchased = true;
      this.purchasedItems.push(item)
    },
  },
};
</script>

<style>
@import "../styles/styles.scss";
</style>