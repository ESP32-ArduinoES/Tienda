<template>
  <div>
    <Navbar />
    <div class="container my-5">
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col" v-for="(item, index) in productos" :key="index">
          <div class="card">
            <img :src="item.foto" class="card-img-top" />
            <div class="card-body">
              <h5 class="card-title text-center">{{ item.nombre }}</h5>
              <p class="card-text text-center">{{ item.familia }}</p>
            </div>
            <div class="container">
              <div class="row">
                <div class="col">
                  <div class="text-start text-primary">
                    <i v-if="item.valoracion === '1'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '2'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '2'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '3'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '3'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '3'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '4'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '4'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '4'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '4'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '5'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '5'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '5'" class="fas fa-star"></i>
                    <i v-if="item.valoracion === '5'" class="fas fa-star"></i>
                    <i
                      v-if="item.valoracion === '5'"
                      class="fas fa-star primary"
                    ></i>
                  </div>
                </div>
                <div class="col text-end">
                  <i>
                    <span class="title is-4 "
                      >{{ item.precio + " " }}<strong>&euro;</strong></span
                    >
                  </i>
                </div>
              </div>
            </div>
            <div class="card-footer btn-actions">
              <div class="card-footer-item field is-grouped">
                <div class="input-group mb-3">
                  <button class="btn btn-outline-secondary" type="button">
                    Añadir al carro
                  </button>
                  <input
                    class="form-control text-center"
                    value="0"
                    id="cantidad"
                    type="number"
                    min="0"
                    max="20"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import { collection, getDocs } from "firebase/firestore/lite";
import { db } from "../main";
export default {
  name: "Home",
  components: {
    Navbar,
  },
  data() {
    return {
      productos: [],
      producto: {
        id: "",
        nombre: "",
        familia: "",
        descripcion: "",
        precio: "",
        valoracion: "",
        unidades: "",
        enlace: "",
        foto: "",
      },
    };
  },
  methods: {
    // GET
    async obtenerDatos() {
      const querySnapshot = await getDocs(collection(db, "productos"));
      querySnapshot.forEach((doc) => {
        let producto = doc.data();
        producto.id = doc.id;
        this.productos.push(producto);
        console.log(producto);
      });
    },
  },
  mounted() {
    this.obtenerDatos();
  },
};
</script>
