<template>
  <main class="py-24 px-80">
    <div class="min-w-full items-center">
      <p class="text-4xl font-bold my-8">Criar novo usuário</p>
      <p class="text-3xl font-bold my-2">Informações:</p>
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Nome*"
        type="text"
        v-model="nome"
      />
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Sobrenome*"
        type="text"
      />
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Telefone*"
        type="tel"
        v-model="telefone"
      />
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Endereco*"
        type="text"
        v-model="endereco"
      />
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Email*"
        type="email"
        v-model="email"
      />
      <input
        class="my-2 w-full p-4 rounded-md outline outline-1 outline-gray-200"
        placeholder="Senha*"
        type="password"
        v-model="password"
        v-on:keyup.enter="register()"
      />
      <button
        class="bg-blue-500 my-4 font-medium text-gray-100 w-full p-4 rounded-xl hover:bg-gray-100 hover:text-blue-500 ease-in-out duration-200"
        @click="register()"
      >
        CADASTRAR
      </button>
    </div>
  </main>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",
      nome: "",
      sobrenome: "",
      telefone: "",
      endereco: "",
    };
  },
  methods: {
    register() {
      axios
        .post("https://back-endgarrafinhas-production.up.railway.app/users/", {
          email: this.email,
          password: this.password,
          first_name: this.nome,
          last_name: this.sobrenome,
          telefone: this.telefone,
          endereco: this.endereco,
        })
        .then((response) => {
          console.log(response);
          if (response.status == 201) {
            this.$router.push("/");
          }
        })
        .catch((error) => {
          if (error.response.status == 400) {
            alert("Email já cadastrado");
          }
          else if (error.response.status == 500) {
            alert("Erro interno do servidor");
          }
          console.log(error);
        });
    },
  },
};
</script>
