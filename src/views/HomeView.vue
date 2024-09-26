<template>
  <main>
    <h1>Szakkörök</h1>
    <div class="split">
      <div class="left">
        <ul class="list-group">
          <li 
            v-for="tanulo in tanulok" 
            :key="tanulo.id" 
            class="list-group-item" 
            @click="selectTanulo(tanulo)"
          >
            {{ tanulo.nev }} ({{ tanulo.osztaly }})
          </li>
        </ul>
        <div class="mt-3">
          <select v-model="kivalasztottSzakkor" id="szakkorValaszto">
            <option v-for="szakkor in szakkorok" :key="szakkor.id" :value="szakkor.nev">
              {{ szakkor.nev }}
            </option>
          </select>
          <button @click="checkSzakkor()">Ellenőrzés</button>
        </div>
      </div>

      <div class="right">
        <div class="card" v-if="selectedTanulo">
          <div class="card-body">
            <h5 class="card-title">{{ selectedTanulo.nev }}</h5>
            <p class="card-text">
              <span v-if="selectedTanulo.jelenlegiSzakkor">{{ selectedTanulo.jelenlegiSzakkor }}</span>
              <span v-else>Nem jár szakkörre</span>
            </p>
            <p class="card-text" v-if="szakkorIsInTanulo()">
              Jelenlegi szakkör: {{ kivalasztottSzakkor }}
            </p>
            <p class="card-text" v-else>
              Az adott tanuló nem jár a szakkörre.
            </p>
          </div>
        </div>
        <p v-else>Kérlek válassz ki egy tanulót!</p>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Jacob Thornton", osztaly: "9.A", jelenlegiSzakkor: "Foci" },
        { id: 2, nev: "Mark Otto", osztaly: "10.B", jelenlegiSzakkor: "Zene" },
        { id: 3, nev: "Larry Bird", osztaly: "11.C", jelenlegiSzakkor: "Programozás" },
        { id: 4, nev: "Anna Smith", osztaly: "9.A", jelenlegiSzakkor: "" },
        { id: 5, nev: "David Johnson", osztaly: "10.B", jelenlegiSzakkor: "" },
        { id: 6, nev: "James Brown", osztaly: "11.C", jelenlegiSzakkor: "" },
        { id: 7, nev: "Emily Davis", osztaly: "9.A", jelenlegiSzakkor: "" },
        { id: 8, nev: "Michael Miller", osztaly: "10.B", jelenlegiSzakkor: "" },
        { id: 9, nev: "Sarah Wilson", osztaly: "11.C", jelenlegiSzakkor: "" },
        { id: 10, nev: "Chris Lee", osztaly: "9.A", jelenlegiSzakkor: "" },
        { id: 11, nev: "Emma Moore", osztaly: "10.B", jelenlegiSzakkor: "" },
        { id: 12, nev: "John Anderson", osztaly: "11.C", jelenlegiSzakkor: "" },
        { id: 13, nev: "Olivia Martinez", osztaly: "9.A", jelenlegiSzakkor: "" },
        { id: 14, nev: "Sophia Thompson", osztaly: "10.B", jelenlegiSzakkor: "" },
        { id: 15, nev: "Mason White", osztaly: "11.C", jelenlegiSzakkor: "" }
      ],
      szakkorok: [
        { id: 1, nev: "Foci" },
        { id: 2, nev: "Zene" },
        { id: 3, nev: "Programozás" }
      ],
      kivalasztottSzakkor: "", 
      selectedTanulo: null,
    };
  },
  methods: {
    selectTanulo(tanulo) {
      this.selectedTanulo = tanulo;
    },
    checkSzakkor() {
      if (this.selectedTanulo) {
        this.selectedTanulo.jelenlegiSzakkor = this.kivalasztottSzakkor;
      }
    },
    szakkorIsInTanulo() {
      return this.selectedTanulo.jelenlegiSzakkor === this.kivalasztottSzakkor;
    }
  }
};
</script>

<style scoped>
h1 {
  text-align: center;
  border: 4px black solid;
}

.split {
  display: flex;
}

.left {
  flex: 40%;
  margin-right: 20px;
}

.right {
  flex: 60%;
}

.card {
  margin-bottom: 10px;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #45a049;
}

.list-group {
  max-height: 300px;
  overflow-y: auto;
}

.card-title {
  margin-bottom: 10px;
}

select {
  padding: 5px;
  margin-top: 10px;
  width: 100%;
}
</style>
