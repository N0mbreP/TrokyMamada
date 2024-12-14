<template>
  <div id="app">
    <h1>Calculadora de Stats Pokémon</h1>
    <table>
      <thead>
        <tr>
          <th>Pokémon</th>
          <th>Nivel Necesario</th>
          <th>Stats Totales</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pokemon in pokemonsCalculados" :key="pokemon.nombre">
          <td>{{ pokemon.nombre }}</td>
          <td>{{ pokemon.nivelNecesario }}</td>
          <td>{{ pokemon.statsTotales }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Lista de Pokémon base (JSON proporcionado)
      pokemons: [
  { "Pokémon": "Shedinja", "Vida": 1, "Ataque": 90, "Defensa": 45, "Ataque Especial": 30, "Defensa Especial": 30, "Velocidad": 40 },
  { "Pokémon": "Mewtwo", "Vida": 106, "Ataque": 110, "Defensa": 90, "Ataque Especial": 154, "Defensa Especial": 90, "Velocidad": 130 },
  { "Pokémon": "Metagross", "Vida": 80, "Ataque": 135, "Defensa": 130, "Ataque Especial": 95, "Defensa Especial": 90, "Velocidad": 70 },
  { "Pokémon": "Abra", "Vida": 25, "Ataque": 20, "Defensa": 15, "Ataque Especial": 105, "Defensa Especial": 55, "Velocidad": 90 },
  { "Pokémon": "Deoxys", "Vida": 50, "Ataque": 150, "Defensa": 50, "Ataque Especial": 150, "Defensa Especial": 50, "Velocidad": 150 },
  { "Pokémon": "Castform", "Vida": 70, "Ataque": 70, "Defensa": 70, "Ataque Especial": 70, "Defensa Especial": 70, "Velocidad": 70 },
  { "Pokémon": "Scyther", "Vida": 70, "Ataque": 110, "Defensa": 80, "Ataque Especial": 55, "Defensa Especial": 80, "Velocidad": 105 },
  { "Pokémon": "Slakoth", "Vida": 60, "Ataque": 60, "Defensa": 60, "Ataque Especial": 35, "Defensa Especial": 35, "Velocidad": 30 },
  { "Pokémon": "Zigzagoon", "Vida": 38, "Ataque": 30, "Defensa": 41, "Ataque Especial": 30, "Defensa Especial": 41, "Velocidad": 60 },
  { "Pokémon": "Seedot", "Vida": 40, "Ataque": 40, "Defensa": 50, "Ataque Especial": 30, "Defensa Especial": 30, "Velocidad": 30 },
  { "Pokémon": "Ralts", "Vida": 28, "Ataque": 25, "Defensa": 25, "Ataque Especial": 45, "Defensa Especial": 35, "Velocidad": 40 },
  { "Pokémon": "Vaporeon", "Vida": 130, "Ataque": 65, "Defensa": 60, "Ataque Especial": 110, "Defensa Especial": 95, "Velocidad": 65 },
  { "Pokémon": "Sableye", "Vida": 50, "Ataque": 75, "Defensa": 75, "Ataque Especial": 65, "Defensa Especial": 65, "Velocidad": 50 },
  { "Pokémon": "Absol", "Vida": 65, "Ataque": 130, "Defensa": 60, "Ataque Especial": 75, "Defensa Especial": 60, "Velocidad": 75 },
  { "Pokémon": "Zangoose", "Vida": 73, "Ataque": 115, "Defensa": 60, "Ataque Especial": 60, "Defensa Especial": 60, "Velocidad": 90 },
  { "Pokémon": "Jirachi", "Vida": 100, "Ataque": 100, "Defensa": 100, "Ataque Especial": 100, "Defensa Especial": 100, "Velocidad": 100 },
  { "Pokémon": "Gastly", "Vida": 30, "Ataque": 35, "Defensa": 30, "Ataque Especial": 100, "Defensa Especial": 35, "Velocidad": 80 },
  { "Pokémon": "Regice", "Vida": 80, "Ataque": 50, "Defensa": 100, "Ataque Especial": 100, "Defensa Especial": 200, "Velocidad": 50 },
  { "Pokémon": "Chimecho", "Vida": 65, "Ataque": 50, "Defensa": 70, "Ataque Especial": 95, "Defensa Especial": 80, "Velocidad": 65 },
  { "Pokémon": "Mew", "Vida": 100, "Ataque": 100, "Defensa": 100, "Ataque Especial": 100, "Defensa Especial": 100, "Velocidad": 100 },
  { "Pokémon": "Feebas", "Vida": 20, "Ataque": 15, "Defensa": 20, "Ataque Especial": 10, "Defensa Especial": 55, "Velocidad": 80 },
  { "Pokémon": "Moltres", "Vida": 90, "Ataque": 100, "Defensa": 90, "Ataque Especial": 125, "Defensa Especial": 85, "Velocidad": 90 },
  { "Pokémon": "Slaking", "Vida": 150, "Ataque": 160, "Defensa": 100, "Ataque Especial": 95, "Defensa Especial": 65, "Velocidad": 100 },
  { "Pokémon": "Seviper", "Vida": 73, "Ataque": 100, "Defensa": 60, "Ataque Especial": 100, "Defensa Especial": 60, "Velocidad": 65 },
  { "Pokémon": "Beedrill", "Vida": 65, "Ataque": 90, "Defensa": 40, "Ataque Especial": 45, "Defensa Especial": 80, "Velocidad": 75 },
  { "Pokémon": "Barboach", "Vida": 50, "Ataque": 48, "Defensa": 43, "Ataque Especial": 46, "Defensa Especial": 41, "Velocidad": 60 },
  { "Pokémon": "Lotad", "Vida": 40, "Ataque": 30, "Defensa": 30, "Ataque Especial": 40, "Defensa Especial": 50, "Velocidad": 30 },
  { "Pokémon": "Gardevoir", "Vida": 68, "Ataque": 65, "Defensa": 65, "Ataque Especial": 125, "Defensa Especial": 115, "Velocidad": 80 },
  { "Pokémon": "Registeel", "Vida": 80, "Ataque": 75, "Defensa": 150, "Ataque Especial": 75, "Defensa Especial": 150, "Velocidad": 50 },
  { "Pokémon": "Latios", "Vida": 80, "Ataque": 90, "Defensa": 80, "Ataque Especial": 130, "Defensa Especial": 110, "Velocidad": 110 },
  { "Pokémon": "Tropius", "Vida": 99, "Ataque": 68, "Defensa": 83, "Ataque Especial": 72, "Defensa Especial": 87, "Velocidad": 51 },
  { "Pokémon": "Pikachu", "Vida": 35, "Ataque": 55, "Defensa": 40, "Ataque Especial": 50, "Defensa Especial": 50, "Velocidad": 90 }
],
      // Resultado calculado
      pokemonsCalculados: []
    };
  },
  mounted() {
    this.calcularStatsParaTodos();
  },
  methods: {
    calcularStat(base, nivel, esHP = false) {
      if (esHP) {
        return Math.floor(((2 * base) / 100) * nivel) + nivel + 10;
      } else {
        return Math.floor(((2 * base) / 100) * nivel) + 5;
      }
    },
    calcularStatsTotales(pokemon, nivel) {
      const hp = this.calcularStat(pokemon.Vida, nivel, true);
      const ataque = this.calcularStat(pokemon.Ataque, nivel);
      const defensa = this.calcularStat(pokemon.Defensa, nivel);
      const ataqueEspecial = this.calcularStat(pokemon["Ataque Especial"], nivel);
      const defensaEspecial = this.calcularStat(pokemon["Defensa Especial"], nivel);
      const velocidad = this.calcularStat(pokemon.Velocidad, nivel);

      return hp + ataque + defensa + ataqueEspecial + defensaEspecial + velocidad;
    },
    calcularStatsParaTodos() {
      this.pokemonsCalculados = this.pokemons.map((pokemon) => {
        let nivel = 1;
        let statsTotales = 0;

        // Incrementa el nivel hasta alcanzar un total cercano a 710
        while (statsTotales < 531 && nivel <= 100) {
          statsTotales = this.calcularStatsTotales(pokemon, nivel);
          if (statsTotales >= 531) break;
          nivel++;
        }

        return {
          nombre: pokemon.Pokémon,
          nivelNecesario: nivel,
          statsTotales: statsTotales
        };
      });
    }
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}
table {
  margin: 20px auto;
  border-collapse: collapse;
  width: 80%;
}
table th, table td {
  border: 1px solid #ddd;
  padding: 8px;
}
table th {
  background-color: #f4f4f4;
}
</style>
