<template>
  <div>
   <v-container>
    <v-row class="text-center">
      <v-col cols="8">
        <v-card>
          <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th>Team (away)</th>
                  <th>Team (home)</th>
                  <th>Score</th>
                  <th>Date</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="match in futureMatches" :key="match.id">
                  <td>{{ match.awayTeam.name }}</td>
                  <td>{{ match.homeTeam.name }}</td>
                  <td>{{ match.score.fullTime.awayTeam }}-{{ match.score.fullTime.homeTeam }}</td>
                  <td>{{ match.utcDate }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card>
      </v-col>
      <v-col cols="4">
        <v-card>
          <v-list>
            <v-list-item-group v-model="selectedTeam" @change="getFutureMatches">
              <v-list-item v-for="team in teams" :key="team.id" :value="team.id">
                  <v-list-item-content>
                    <v-list-item-title>{{ team.shortName }}</v-list-item-title> 
                  </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
          <!-- <v-text-field placeholder="Search a team" class="px-4" /> -->
        </v-card>
      </v-col>
    </v-row>
   </v-container>
  </div>
</template>

<script>
import axios from 'axios'

const config = { headers: { 'X-Auth-Token': '0eff9909ec3f4ef79bc75ee75c1470ef' } }

// list of all our teams
// list of the selected team's future matches
// if someone selects another team, replace the future matches

export default {
  name: 'Teams',
  data: () => ({
    teams: [],
    futureMatches: [],
    selectedTeam: 1
  }),
  mounted () {
    this.getTeams()
    this.getAllCompetitions()
  },
  methods: {
    getTeams () {
      return axios.get('http://api.football-data.org/v2/competitions/CL/teams/', config).then((result) => {
        this.teams = result.data.teams
      })
    },
    getFutureMatches () {
      const id = this.selectedTeam
      return axios.get(`http://api.football-data.org/v2/teams/${id}/matches/`, config).then((result) => {
        this.futureMatches = result.data.matches
      })
    },
    getAllCompetitions () {
      return axios.get(`http://api.football-data.org/v2/competitons/`, config).then((result) => {
        console.log(result.data.competitions)
      })
    }
  }
}

</script>