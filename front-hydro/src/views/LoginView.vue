<template>
  <main class="w-screen h-screen">
    <div class="flex flex-row">
      <div class="flex bg-gray-200 w-screen h-screen p-24">
        <div class="min-w-full items-center">
          <p class="text-4xl font-bold my-4">Login</p>
          <p class="text-3xl font-bold my-1">Cliente Registrado</p>
          <input
            class="my-10 w-full p-4 rounded-md"
            placeholder="Email*"
            type="email"
            v-model="email"
          />
          <input
            class="w-full p-4 rounded-md"
            placeholder="Senha*"
            type="password"
            v-model="password"
            v-on:keyup.enter="login()"
          />
          <div class="w-full p-2 flex justify-center">
            <input class="" type="checkbox" />
            <p class="ml-2">Lembre de mim</p>
            <a href="" class="text-blue-500 font-medium ml-10"
              >Esqueceu sua senha?</a
            >
          </div>
          <button
            class="bg-blue-500 font-medium text-gray-100 w-full p-4 rounded-xl hover:bg-gray-100 hover:text-blue-500 ease-in-out duration-200"
            @click="login()"
          >
            LOGIN
          </button>
        </div>
      </div>
      <div
        class="flex justify-center items-center bg-blue-300 w-screen h-screen p-24"
      >
        <p class="text-3xl font-bold my-4 text-gray-100">Novos Clientes</p>
        <button
          class="bg-gray-100 font-medium my-6 text-blue-500 w-full p-4 rounded-xl hover:bg-blue-500 hover:text-gray-100 ease-in-out duration-200"
          @click="
            () => {
              this.$router.push('/register');
            }
          "
        >
          CADASTRE-SE
        </button>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import navbarvue from "@/components/NavBar.vue";
export default {
  components: {
    NavBarVue: navbarvue,
  },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      axios
        .post("https://back-endgarrafinhas-production.up.railway.app/token/", {
          email: this.email,
          password: this.password,
        })
        .then((res) => {
          this.$cookies.set("token", res.data.access);
          this.$router.push("/home");
        })
        .catch((err) => {
          if (err.response.status == 401) {
            alert("Email ou senha incorretos");
          }
          else {
            alert("Erro desconhecido");
          }
          console.log(err);
        });
    },
  },
  mounted() {
    if (this.$cookies.get("token")) {
      this.$router.push("/home");
    }
  },
};
</script>
