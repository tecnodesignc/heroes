<template>
  <q-page class="flex flex-center">
    <div class="q-container q-py-xl">
      <div class="row">
        <div class="col-12 q-pb-xl">
          <q-input v-model="filter" filled clearable dense type="search" label="Buscar personaje"
                   style=" margin:auto; width: 90%; max-width: 500px">
            <template v-slot:append>
              <q-icon name="search"/>
            </template>
          </q-input>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <q-table
            grid
            :data="data"
            :columns="columns"
            row-key="name"
            :filter="filter"
            hide-header
            :pagination="initialPagination"
          >

            <template v-slot:item="props">
              <div class="q-pa-xs col-xs-12 col-sm-6 col-md-4">

                <q-card>
                  <img :src="props.row.images.md">
                  <q-card-section>
                    <div class="text-h6 text-primary text-center">{{ props.row.name }}</div>
                  </q-card-section>
                  <q-card-section>
                    <div>Intelligence: <strong>{{ props.row.powerstats.intelligence }}</strong></div>
                    <div>Speed: <strong>{{ props.row.powerstats.speed }}</strong></div>
                    <div>Power: <strong>{{ props.row.powerstats.power }}</strong></div>
                    <div>Gender: <strong>{{ props.row.appearance.gender }}</strong></div>
                    <div>Race: <strong>{{ props.row.appearance.race }}</strong></div>
                  </q-card-section>
                </q-card>
              </div>
            </template>

          </q-table>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>

import axios from 'axios'

export default {
  name: 'PageIndex',
  components: {},
  mounted () {
    this.$nextTick(function () {
      this.init()
    })
  },
  data () {
    return {
      filter: '',
      initialPagination: {
        sortBy: 'desc',
        descending: false,
        page: 1,
        rowsPerPage: 6
        // rowsNumber: xx if getting data from a server
      },
      columns: [
        {
          name: 'name',
          required: true,
          label: 'Name',
          align: 'center',
          field: row => row.name,
          format: val => `${val}`,
          sortable: true
        },
        {
          name: 'intelligence',
          required: true,
          label: 'Intelligence',
          align: 'left',
          field: row => row.powerstats.intelligence,
          format: val => `${val}`,
          sortable: true
        },
        {
          name: 'speed',
          align: 'left',
          label: 'Speed',
          field: row => row.powerstats.speed,
          sortable: true
        },
        {
          name: 'power',
          label: 'Power',
          field: row => row.powerstats.power,
          sortable: true
        },
        {
          name: 'gender',
          label: 'Gender',
          field: row => row.appearance.gender
        },
        {
          name: 'race',
          label: 'Race',
          field: row => row.appearance.race
        },
        {
          name: 'image',
          label: 'Image',
          field: row => row.images.md
        }
      ],
      data: []
    }
  },
  methods: {
    async init () {
      await this.getData()
    },

    getData () {
      return new Promise((resolve, reject) => {
        axios.get('https://cdn.jsdelivr.net/gh/akabab/superhero-api@0.3.0/api/all.json')
          .then((response) => {
            this.data = response.data
            resolve(true)
          })
      })
    }
  }
}
</script>
