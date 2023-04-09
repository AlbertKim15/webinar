<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="3" md="3">
      <v-card width="350px" class="logo py-4 d-flex justify-center">
        <v-form
        v-model="form"
        ref="form"
        @submit.prevent="onSubmit"
        >
          <v-card-title primary-title class="d-flex justify-center">
          Авторизация</v-card-title>
          
          <v-text-field
          width="200px"
          label="E-mail"
          outlined
          placeholder="test@test.com"
          :readonly="loading"
          :rules="[emailRules, required]"
          v-model="email"></v-text-field>   
          
          <v-text-field
          label="Пароль"
          v-model="name"
          type="password"
          outlined
          :readonly="loading"
          :rules="[required]"
          ></v-text-field>
          <v-btn 
          :disabled="!form"
          :loading="loading"
          block
          color="blue"
          to="/webinar"
          >Авторизация</v-btn>
        </v-form>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',

  data: () => ({
    form: false,
    email: null,
    name: null,
    loading: false,
    emailRules:v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'Не верный формат E-mail',
  }),
  methods: {
      onSubmit () {
        if (!this.form) return

        this.loading = true

        setTimeout(() => (this.loading = false), 2000)
      },
      required (v) {
        return !!v || 'Обязательно к заполнению'
      },
    },
}
</script>
