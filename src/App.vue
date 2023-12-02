<template>
  <div class="gallery-wrapper bg-salmon">
    <div class="title-with-logo">
      <img src="https://logos-world.net/wp-content/uploads/2023/04/Hello-Kitty-Logo.png" alt="Hello Kitty Logo" class="hello-kitty-logo" />
      <h1 class="gallery-title">¡Feliz cumpleaños amor!</h1>
    </div>
    <div class="gallery-container shadow-sm rounded">
      <div v-if="images.length" class="image-container">
        <transition name="fade" mode="out-in">
          <img :key="currentImageIndex" :src="images[currentImageIndex]" :alt="'Imagen ' + (currentImageIndex + 1)" class="gallery-image img-fluid rounded-top" />
        </transition>
      </div>
      <div class="button-container my-3">
        <button class="btn btn-outline-dark btn-sm mx-2" @click="prevImage" :disabled="currentImageIndex === 0">
          Prev
        </button>
        <button class="btn btn-outline-dark btn-sm mx-2" @click="nextImage" :disabled="currentImageIndex === images.length - 1">
          Next
        </button>
      </div>
      <div class="thumbnails d-flex flex-wrap justify-content-center">
        <img v-for="(image, index) in images" :key="'thumb-' + index" :src="image"
             :alt="'Thumbnail ' + (index + 1)" @click="setCurrentImage(index)"
             class="img-thumbnail m-1 rounded" :class="{ 'opacity-50': currentImageIndex !== index, 'opacity-100': currentImageIndex === index }" />
      </div>
    </div>
    <p class="dedication-text">
  Mi amor precioso, mi vida entera<br>
  En este día tan especial, tu 21° cumpleaños, quiero expresarte todo el amor y admiración que siento por ti. Cada momento a tu lado es un regalo invaluable, y cada recuerdo que hemos construido juntos es un tesoro que guardo en el corazón. Eres la luz que ilumina mis días, y no hay nada que desee más que brindarte la felicidad que mereces.<br>
  Estoy agradecido por cada sonrisa que compartimos, por cada sueño que tejemos y por cada desafío que superamos juntos. Que este nuevo capítulo de tu vida esté lleno de alegrías, descubrimientos y momentos tan hermosos como los que me has dado. Prometo seguir construyendo una relación tan bonita y amorosa como tú.<br>
  Con todo mi amor,<br>
  Tu amorcito<br>
</p>
  </div>
  <div class="youtube-video-container">
      <iframe
        width="560"
        height="315"
        :src="youtubeEmbedUrl"
        title="YouTube video player"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
    </div>
</template>

<script>
import img1 from '@/assets/img1.jpg'; // Asegúrate de que las rutas sean correctas
import img2 from '@/assets/img2.jpg';
import img3 from '@/assets/img3.jpg';

export default {
  name: 'PhotoGallery',
  data() {
    return {
      currentImageIndex: 0,
      images: [img1, img2, img3],
      youtubeEmbedUrl: 'https://www.youtube.com/embed/R6FgTjh5xq0',
    };
  },
  methods: {
    nextImage() {
      if (this.currentImageIndex < this.images.length - 1) {
        this.currentImageIndex++;
      }
    },
    prevImage() {
      if (this.currentImageIndex > 0) {
        this.currentImageIndex--;
      }
    },
    setCurrentImage(index) {
      this.currentImageIndex = index;
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Handlee&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

.gallery-wrapper {
  background-color: #FCE4EC; /* Un rosa claro que podría asociarse con Hello Kitty */
  padding: 2rem;
  text-align: center;
  font-family: 'Handlee', cursive; /* Fuente manuscrita que es lúdica y amigable */
}

.dedication-text {
  font-family: 'Pacifico', cursive;
  font-size: 1.5rem; /* Un tamaño de fuente grande y legible */
  color: #000;
  text-align: center;
  margin-top: 1rem;
  margin-bottom: 2rem; /* Espacio antes y después del texto de dedicatoria */
}
.gallery-title {
  margin: 0; /* Elimina el margen predeterminado */
  display: inline-block; /* Hace que el título se comporte como un elemento en línea para trabajar con flexbox */
  font-size: 4rem;
  color: #000; /* Espacio entre el título y la galería */
}

.gallery-container {
  background-color: #fff; /* Fondo blanco para la galería */
  border: 5px solid #FCE4EC; /* Borde rosa para la galería */
  border-radius: 1rem; /* Bordes más redondeados */
}

.image-container {
  position: relative;
  z-index: 9;
}

.gallery-image {
  max-width: 100%;
  height: auto;
  border-radius: 1rem 1rem 0 0; /* Bordes más redondeados en la parte superior */
}

.button-container {
  text-align: center;
}

.img-thumbnail {
  width: 100px;
  height: auto;
  object-fit: cover;
  border-color: rgba(255, 255, 255, 0.7);
  border-radius: 0.5rem; /* Bordes redondeados para las miniaturas */
}

.opacity-50 {
  opacity: 0.5;
}

.opacity-100 {
  opacity: 1;
}

.text-light {
  color: #fff;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: scale(0.95);
}
.title-with-logo {
  position: relative; /* Esto asegura que el logo se posicione en relación con este contenedor */
  display: flex; /* Utilizamos flexbox para alinear el logo y el título */
  align-items: center; /* Centra el logo y el título verticalmente */
  justify-content: center; /* Centra el logo y el título horizontalmente */
  gap: 1rem; /* Espacio entre el logo y el título */
}

.hello-kitty-logo {
  position: relative; /* Posición relativa para que no se desplace fuera del contenedor */
  width: 100px; /* O el tamaño que prefieras */
  height: auto; /* Mantiene la relación de aspecto */
}

/* Estilos adicionales para los botones con tema de Hello Kitty */
.btn-hello-kitty {
  background-color: #FCE4EC; /* Rosa claro de Hello Kitty */
  color: #000;
  border-color: #FCE4EC;
  border-radius: 20px; /* Botones con bordes redondeados */
  transition: background-color 0.3s, color 0.3s;
}

.btn-hello-kitty:hover {
  background-color: #F06292; /* Un rosa más fuerte para el hover */
  color: #fff;
}

.youtube-video-container {
  text-align: center; /* Centra el iframe del video */
  margin-top: 1rem;
}

.youtube-video-container iframe {
  max-width: 100%; /* Hace que el video sea responsivo */
  border-radius: 0.5rem; /* Bordes redondeados para el iframe */
}

/* Puedes agregar detalles específicos de Hello Kitty como bordes, sombras o decoraciones adicionales */
/* Por ejemplo, un borde rojo o un pequeño gráfico de Hello Kitty en una esquina (si tienes permiso para usar la imagen) */
</style>