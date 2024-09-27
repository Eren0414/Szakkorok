<template>
  <main class="my-container">
    <h1 class="sticky-top">Diákok és a Szakkörök</h1>
    <div class="row">
      <div class="col-5">
        <!-- Diákok táblázat -->
        <table class="table">
          <thead>
            <tr>
              <th scope="col">Diákok</th>
              <th scope="col">Osztályok</th>
              <th scope="col">Szakkörök</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="tanulo in sortedTanulok" :key="tanulo.id">
              <td class="my-td">{{ tanulo.nev }}</td>
              <td class="my-td">{{ tanulo.osztaly }}</td>
              <td>
                <select class="form-select" v-model="tanulo.szakkorId" @change="addTanuloToSzakkor(tanulo)">
                  <option v-for="szakkor in szakkorok" :key="szakkor.id" :value="szakkor.id">
                    {{ szakkor.nev }}
                  </option>
                </select>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="col-7 px-5">
        <div class="sticky-top">
          <!-- Szakkörök -->
          <h2>Szakkörök</h2>
          <ProfessionCard
          v-for="(szakkor) in szakkorok" :key="szakkor.id"
          :szakkor="szakkor"
          :tanulok="tanulok"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import ProfessionCard from '@/components/ProfessionCard.vue';

export default {
  components: {
    ProfessionCard
  },
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Kovács Péter", osztaly: "9.A", szakkorId: 4 },
        { id: 2, nev: "Szabó Anna", osztaly: "10.B", szakkorId: 4 },
        { id: 3, nev: "Nagy Gábor", osztaly: "11.C", szakkorId: 4 },
        { id: 4, nev: "Tóth Katalin", osztaly: "9.A", szakkorId: 4 },
        { id: 5, nev: "Varga Tamás", osztaly: "10.B", szakkorId: 4 },
        { id: 6, nev: "Horváth Zoltán", osztaly: "11.C", szakkorId: 4 },
        { id: 7, nev: "Balogh Eszter", osztaly: "10.B", szakkorId: 4 },
        { id: 8, nev: "Molnár Ádám", osztaly: "9.A", szakkorId: 4 },
        { id: 9, nev: "Kocsis László", osztaly: "10.B", szakkorId: 4 },
        { id: 10, nev: "Papp Júlia", osztaly: "11.C", szakkorId: 4 },
        { id: 11, nev: "Kerekes Ferenc", osztaly: "10.B", szakkorId: 4 },
        { id: 12, nev: "Farkas Anikó", osztaly: "11.C", szakkorId: 4 },
        { id: 13, nev: "Kiss István", osztaly: "9.A", szakkorId: 4 },
        { id: 14, nev: "Sipos Emese", osztaly: "11.C", szakkorId: 4 },
        { id: 15, nev: "Rácz Balázs", osztaly: "10.B", szakkorId: 4 }
      ],
      szakkorok: [
        { id: 1, nev: "Foci" },
        { id: 2, nev: "Zene" },
        { id: 3, nev: "Programozás" },
        { id: 4, nev: "Nem jár szakkörre" },
      ],
      szakkorTanulok: {
        Foci: [],
        Zene: [],
        Programozás: []
      }
    };
  },
  computed: {
    sortedTanulok(){
      return this.tanulok.sort((a, b) => a.nev.localeCompare(b.nev))
    },
  },
  methods: {
    addTanuloToSzakkor(tanulo) {
      for (let szakkor in this.szakkorTanulok) {
        const index = this.szakkorTanulok[szakkor].indexOf(tanulo.nev);
        if (index !== -1) {
          this.szakkorTanulok[szakkor].splice(index, 1);
        }
      }

      if (tanulo.szakkorId) {
        this.szakkorTanulok[tanulo.szakkorId].push(tanulo.nev);
      }
    }
  }
};
</script>


<style scoped>
.my-container {
  background-image: url("https://htmlcolorcodes.com/assets/images/html-color-codes-color-tutorials-hero.jpg");
  background-size: cover;
  background-position: center;
  padding: 30px;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.row {
  background-color: rgba(0, 0, 0, 0.7); 
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.my-td {
  color: white;
}

h1 {
  color: aquamarine;
  text-align: center;
  border-bottom: 2px solid white;
  padding-bottom: 10px;
  margin-bottom: 20px;
  margin-right: 20px;
  font-family: 'Arial', sans-serif;
  font-size: 2.5rem;
}

h2 {
  text-align: center;
  color: white;
  margin-bottom: 20px;
  font-family: 'Arial', sans-serif;
  font-size: 1.8rem;
}

.table {
  width: 100%;
  margin: 0 auto;
  border-collapse: collapse;
  background-color: rgba(255, 255, 255, 0.1);
}

.table th {
  background-color: rgba(0, 0, 0, 0.8); 
  color: #ffdd57; 
  font-weight: bold;
  padding: 12px 15px;
}

.table td {
  background-color: rgba(255, 255, 255, 0.2); 
  padding: 12px 15px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.table tr:nth-child(even) td {
  background-color: rgba(255, 255, 255, 0.1); 
}

.table tr:hover td {
  background-color: rgba(255, 255, 255, 0.3); 
}

.form-select {
  background-color: #222;
  color: #ffdd57;
  border: 1px solid #ffdd57;
  border-radius: 5px;
  margin-right: 20px;
  font-size: 1rem;
  transition: all 0.3s ease;
}

.form-select:hover, .form-select:focus {
  border-color: #ff6f47;
  outline: none;
}

.sticky-top {
  position: sticky;
  top: 10px;
}

.card {
  background-color: chocolate;
  color: antiquewhite;
  border: 1px solid #ffdd57;
  border-radius: 10px;
  padding: 15px;
  margin-bottom: 20px;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
}

@media (max-width: 768px) {
  .col-5, .col-7 {
    flex: 100%;
    max-width: 100%;
  }
  .row {
    flex-direction: column;
  }
}
</style>

