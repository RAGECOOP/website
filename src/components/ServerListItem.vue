<template>
  <v-dialog v-model="dialog">
    <template v-slot:activator="{ props }">
      <tr v-bind:="props">
        <td>{{ server.name }}</td>
        <td>{{ server.address }}:{{ server.port }}</td>
        <td>{{ server.version }}</td>
        <td><span class="font-weight-medium">{{ server.players }}</span>/{{ server.maxPlayers > 999 ? '∞' : server.maxPlayers }}</td>
        <td>{{ server.country ?? '???' }}</td>
      </tr>
    </template>

    <v-card>
      <v-toolbar :title="server.name" />
      <v-card-text>
        <v-row>
          <v-col :cols="cols[0]">
            <div>
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[0]") }}</span> {{ server.players }}/{{ server.maxPlayers > 999 ? '∞' : server.maxPlayers }}
            </div>
            <div v-show="server.language">
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[1]") }}</span> {{ server.language ?? null }}
            </div>
            <div>
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[2]") }}</span> {{ server.address }}:{{ server.port }}
            </div>
            <div v-show="server.gameMode">
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[3]") }}</span> {{ server.gameMode ?? null }}
            </div>
            <div v-show="server.website">
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[4]") }}</span> {{ server.website ?? null }}
            </div>
            <div v-show="server.description">
              <span class="font-weight-medium text-uppercase">{{ $t("servers[0].tables[0].modal[5]") }}</span> {{ server.description ?? null }}
            </div>
          </v-col>

          <v-col :cols="cols[1]">
            <playerChartComponent :stats="server.playerStats.players" />
            <small>Highest player count for the last 60 minutes (every 10 minutes)</small>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-btn color="error" block @click="dialog = false">{{ $t("servers[0].tables[0].modal[6]") }}</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import playerChartComponent from '@/components/PlayerChart.vue'

export default {
  data: () => ({
    dialog: false
  }),
  props: ["server"],
  components: {
    playerChartComponent
  },
  beforeCreate() {
    this.dialog = true
  },
  computed: {
    cols() {
      const { xl, lg, md } = this.$vuetify.display
      if (xl || lg) return [6, 6]
      if (md) return [5, 7]
      return [12, 12]
    }
  }
}
</script>