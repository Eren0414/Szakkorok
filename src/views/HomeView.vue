<template>
  <main>
    <h1>Szakkörök</h1>
    <div class="split">
      <div class="left">
        <table class="table col-6">
          <thead>
            <tr>
              <th scope="col">Diákok</th>
              <th scope="col">Osztályok</th>
              <th scope="col">Szakkörök</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="tanulo in tanulok" :key="tanulo.id">
              <td>{{ tanulo.nev }}</td>
              <td>{{ tanulo.osztaly }}</td>
              <td>
                <select v-model="tanulo.kivalasztottSzakkor" @change="addTanuloToSzakkor(tanulo)">
                  <option v-for="szakkor in szakkorok" :key="szakkor.id" :value="szakkor.nev">
                    {{ szakkor.nev }}
                  </option>
                </select>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="right">
        <div class="card" v-for="(tanulok, szakkor) in szakkorFeladatok" :key="szakkor">
          <div class="card-body">
            <h5 class="card-title">{{ szakkor }}</h5>
            <p v-if="tanulok.length">
              Tanulók: {{ tanulok.join(', ') }}
            </p>
            <p v-else>Nincs tanuló ebben a szakkörben</p>
          </div>
        </div>
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Még nincs szakköre</h5>
            <p v-if="noSzakkorTanulok.length">
              Tanulók: {{ noSzakkorTanulok.join(', ') }}
            </p>
            <p v-else>Minden tanulónak van szakköre.</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Kovács Péter", osztaly: "9.A", kivalasztottSzakkor: "" },
        { id: 2, nev: "Szabó Anna", osztaly: "10.B", kivalasztottSzakkor: "" },
        { id: 3, nev: "Nagy Gábor", osztaly: "11.C", kivalasztottSzakkor: "" },
        { id: 4, nev: "Tóth Katalin", osztaly: "9.A", kivalasztottSzakkor: "" },
        { id: 5, nev: "Varga Tamás", osztaly: "10.B", kivalasztottSzakkor: "" },
        { id: 6, nev: "Horváth Zoltán", osztaly: "11.C", kivalasztottSzakkor: "" },
        { id: 7, nev: "Balogh Eszter", osztaly: "10.B", kivalasztottSzakkor: "" },
        { id: 8, nev: "Molnár Ádám", osztaly: "9.A", kivalasztottSzakkor: "" },
        { id: 9, nev: "Kocsis László", osztaly: "10.B", kivalasztottSzakkor: "" },
        { id: 10, nev: "Papp Júlia", osztaly: "11.C", kivalasztottSzakkor: "" },
        { id: 11, nev: "Kerekes Ferenc", osztaly: "10.B", kivalasztottSzakkor: "" },
        { id: 12, nev: "Farkas Anikó", osztaly: "11.C", kivalasztottSzakkor: "" },
        { id: 13, nev: "Kiss István", osztaly: "9.A", kivalasztottSzakkor: "" },
        { id: 14, nev: "Sipos Emese", osztaly: "11.C", kivalasztottSzakkor: "" },
        { id: 15, nev: "Rácz Balázs", osztaly: "10.B", kivalasztottSzakkor: "" }
      ],
      szakkorok: [
        { id: 1, nev: "Foci" },
        { id: 2, nev: "Zene" },
        { id: 3, nev: "Programozás" }
      ],
      szakkorFeladatok: {
        Foci: [],
        Zene: [],
        Programozás: []
      }
    };
  },
  computed: {
    noSzakkorTanulok() {
      return this.tanulok
        .filter(tanulo => !tanulo.kivalasztottSzakkor)
        .map(tanulo => tanulo.nev);
    }
  },
  methods: {
    addTanuloToSzakkor(tanulo) {
      // Remove the student from all szakkorok
      for (let szakkor in this.szakkorFeladatok) {
        const index = this.szakkorFeladatok[szakkor].indexOf(tanulo.nev);
        if (index !== -1) {
          this.szakkorFeladatok[szakkor].splice(index, 1);
        }
      }

      // If a szakkor is selected, add the student to the chosen szakkor
      if (tanulo.kivalasztottSzakkor) {
        this.szakkorFeladatok[tanulo.kivalasztottSzakkor].push(tanulo.nev);
      }
    }
  }
};
</script>


<style scoped>
.table {
  max-width: 600px;
}

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
  border-right: 2px solid black; 
  padding-right: 10px; 
}

.right {
  flex: 60%;
}

.card {
  margin-bottom: 10px;
  width: 450px;
}

select {
  padding: 5px;
  margin-top: 5px;
}
</style>
