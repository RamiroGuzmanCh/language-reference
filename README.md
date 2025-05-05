# 🎬 Vue 3 + PrimeVue + Vite + i18n + TVMaze API

Guía paso a paso para crear una aplicación Vue 3 usando PrimeVue, `vue-i18n`, y consumiendo datos desde la [TVMaze API](https://api.tvmaze.com/).
## 📁 Estructura del Proyecto

El proyecto debe tener la siguiente estructura:

```
lastpractice
│
├── src
│   ├── locales
│   │   ├── en.json
│   │   └── es.json
│   ├── assets
│   │   ├── base.css
│   │   ├── logo.svg
│   │   └── main.css
│   │
│   ├── episodes
│   │   ├── components
│   │   │   ├── episodes-item.component.vue
│   │   │   └── episodes-list.component.vue
│   │   ├── model
│   │   │   └── episodes.entity.js
│   │   ├── services
│   │   │   ├── episodes.assembler.js
│   │   │   └── episodes-api.service.js
│   └── public
│   │   ├── footer-content.component.vue
│   │   └── language-switcher.component.vue
│   │
├── App.vue
├── i18n.js
└── main.js
```

---


---

## 📦 Sección 1: package.json

```json
{
  "name": "lastpractice",
  "version": "0.0.0",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@primevue/themes": "^4.3.3",
    "axios": "^1.8.4",
    "primeflex": "^4.0.0",
    "primeicons": "^7.0.0",
    "primevue": "^4.3.3",
    "vue": "^3.5.13",
    "vue-i18n": "^10.0.7"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.2.3",
    "vite": "^6.2.4",
    "vite-plugin-vue-devtools": "^7.7.2"
  }
}
```

---

## 🌍 Sección 2: Archivos de Traducción (`locales/`)

### 📄 locales/en.json

```json
{
  "episodes": {
    "id": "Nro.",
    "url": "Url",
    "name": "Name",
    "season": "Season",
    "number": "Number",
    "type": "Type",
    "airdate": "AirDate",
    "airtime": "AirTime",
    "airstamp": "AirStamp",
    "runtime": "RunTime",
    "rating": "Rating",
    "image": "Image",
    "medium": "Medium",
    "original": "Original",
    "summary": "Summary",
    "_links": "Links",
    "href": "href",
    "show": "Show",
    "https://api.tvmaze.com/shows/1": "https://api.tvmaze.com/shows/1",
    "sname": "Name",
    "episode": "Episode"
  },
  "authoring-phrase": {
    "intro": "Made with",
    "use": "using",
    "author": "by U202217212 -  Mauricio Muñoz Vilcapoma"
  },
  "footer": {
    "powered-by": "Powered by",
    "and": "and"
  }
}
```

### 📄 locales/es.json

```json
{
  "episodes": {
    "id": "Nro.",
    "url": "Enlace",
    "name": "Nombre",
    "season": "Temporada",
    "number": "Episodio",
    "type": "Tipo",
    "airdate": "Fecha de emisión",
    "airtime": "Hora de emisión",
    "airstamp": "Fecha y hora exacta",
    "runtime": "Duración",
    "rating": "Puntuación",
    "image": "Imagen",
    "medium": "Tamaño mediano",
    "original": "Tamaño original",
    "summary": "Resumen",
    "_links": "Enlaces",
    "href": "href",
    "show": "Show",
    "https://api.tvmaze.com/shows/1": "https://api.tvmaze.com/shows/1",
    "sname": "Nombre del show",
    "episode": "Episodio"
  },
  "authoring-phrase": {
    "intro": "Hecho con",
    "use": "usando",
    "author": "por U202217212 - Mauricio Muñoz Vilcapoma"
  },
  "footer": {
    "powered-by": "Desarrollado por",
    "and": "y"
  }
}
```

---

## 🌐 Sección 3: Configuración i18n (`i18n.js`)

```js
import { createI18n } from "vue-i18n";
import en from "./locales/en.json";
import es from "./locales/es.json";

const i18n = createI18n({
  legacy: false,
  locale: 'en',
  globalInjection: true,
  messages: { en, es }
});

export default i18n;
```

---

## 🚀 Sección 4: main.js

```js
import './assets/main.css'

import { createApp } from 'vue'
import App from './App.vue'
import i18n from "@/i18n.js";
import PrimeVue from "primevue/config";
import {Avatar, Button, Card, Drawer, Menu, Menubar, SelectButton, Toolbar, Tooltip} from 'primevue';
import Material from '@primevue/themes/material';

const app = createApp(App);
app
  .use(PrimeVue, { ripple: true, theme:{ preset: Material }})
  .component('pv-button', Button)
  .component('pv-card', Card)
  .component('pv-select-button', SelectButton)
  .component('pv-drawer', Drawer)
  .component('pv-avatar', Avatar)
  .component('pv-menu', Menu)
  .component('pv-menubar', Menubar)
  .component('pv-toolbar', Toolbar)
  .component('pv-tooltip', Tooltip)
  .use(i18n)
  .mount("#app");
```

---

## 📌 Sección 5: Componentes Públicos (`/public`)

### footer-content.component.vue

```vue
<template>
  <div class="grid bg-primary mt-4 align-content-start">
    <div class="col-12 ml-3">
      <p>Copyright 2025. ACME Studios</p>
      <p>
        {{ $t('authoring-phrase.intro')}} <i class="pi pi-heart"/>
        {{ $t('authoring-phrase.use')}} <a href="https://primevue.org/" target="_blank">Prime Vue</a>
        {{ $t('authoring-phrase.author') }}
      </p>
      <p>
        {{ $t('footer.powered-by') }} <a href="https://www.newsapi.org/">NewsAPI.org</a>
        {{ $t('footer.and') }} <a href="https://www.clearbit.com">Clearbit Logo API</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "footer-content"
}
</script>
```

### language-switcher.component.vue

```vue
<template>
  <pv-select-button v-model="$i18n.locale" :options="languages" class="uppercase"/>
</template>

<script>
export default {
  name: "language-switcher",
  data() {
    return {
      languages: ['en', 'es'],
      language: 'en'
    };
  }
};
</script>
```

---

## 🧠 Sección 6: Entidad de Episodio (`episodes.entity.js`)

```js
export class Episodes {
  constructor({
    id = "", url = "", name = "", season = "", number = "", type = "",
    airdate = "", airtime = "", airstamp = "", runtime = "",
    rating = { average: "" }, image = { medium: "", original: "" },
    summary = "", _links = { self: { href: "" }, show: { href: "", name: "" } }
  }) {
    this.id = id;
    this.url = url;
    this.name = name;
    this.season = season;
    this.number = number;
    this.type = type;
    this.airdate = airdate;
    this.airtime = airtime;
    this.airstamp = airstamp;
    this.runtime = runtime;
    this.rating = rating?.average ?? "";
    this.imageMedium = image?.medium ?? "";
    this.imageOriginal = image?.original ?? "";
    this.summary = summary;
    this.linkSelf = _links?.self?.href ?? "";
    this.linkShow = _links?.show?.href ?? "";
    this.showName = _links?.show?.name ?? "";
  }
}
```

---

## 🔨 Sección 7: Assembler (`episodes.assembler.js`)

```js
import { Episodes } from "@/episodes/model/episodes.entity.js";

export class EpisodesAssembler {
  static toEntitiesFromResponse(response) {
    if (!response || !Array.isArray(response)) {
      console.error("Invalid API data");
      return [];
    }

    return response.map(this.toEntityFromResource);
  }

  static toEntityFromResource(resource) {
    return new Episodes(resource);
  }
}
```

---

## 🔗 Sección 8: Servicio API (`episodes-api.service.js`)

```js
import { EpisodesAssembler } from "@/episodes/services/episodes.assembler.js";
import axios from "axios";

export class EpisodesApiService {
  async getEpisodes() {
    const response = await axios.get("https://api.tvmaze.com/shows/1/episodes");
    return EpisodesAssembler.toEntitiesFromResponse(response.data.episodes);
  }
}
```

---

## 🧩 Sección 9: Componentes

### episodes-item.component.vue

```vue
<template>
  <div class="episode-card">
    <img :src="episodes.imageMedium" :alt="episodes.name" class="episode-img"/>
    <div class="episode-content">
      <h2>{{ episodes.name }}</h2>
      <p>{{ $t('episodes.season') }} {{ episodes.season }},
         {{ $t('episodes.rating') }} {{ episodes.rating }}</p>
      <div v-html="episodes.summary"></div>
      <div>
        <a :href="episodes.url" target="_blank">Ver en TVMaze</a>
        <button @click="shareEpisodes">Compartir</button>
      </div>
    </div>
  </div>
</template>

<script>
import { Episodes } from "@/episodes/model/episodes.entity.js";

export default {
  name: "Episodes-Item",
  props: {
    episodes: {
      type: Episodes,
      required: true
    }
  },
  methods: {
    async shareEpisodes() {
      const shareData = {
        name: this.episodes.name,
        url: this.episodes.linkShow
      };
      console.log("Sharing episode:", shareData);
    }
  }
};
</script>
```

---

### episodes-list.component.vue

```vue
<template>
  <div class="episodes-grid">
    <EpisodesItem v-for="episode in episodes" :key="episode.id" :episodes="episode" />
  </div>
</template>

<script>
import EpisodesItem from "@/episodes/components/episodes-item.component.vue";

export default {
  name: "EpisodesList",
  components: { EpisodesItem },
  props: {
    episodes: {
      type: Array,
      required: true
    }
  }
};
</script>
```

---

## 🧩 Sección 10: App.vue

```vue
<template>
  <div>
    <pv-menubar>
      <template #start>
        <pv-button icon="pi pi-bars" label="Episodes Store API Shows" text />
      </template>
      <template #end>
        <language-switcher/>
      </template>
    </pv-menubar>

    <episodes-list :episodes="episodes"/>
    <footer-content/>
  </div>
</template>

<script>
import LanguageSwitcher from "@/public/language-switcher.component.vue";
import FooterContent from "@/public/footer-content.component.vue";
import EpisodesList from "@/episodes/components/episodes-list.component.vue";
import { EpisodesApiService } from "@/episodes/services/episodes-api.service.js";
import { defineComponent } from "vue";

export default defineComponent({
  components: { EpisodesList, LanguageSwitcher, FooterContent },
  data() {
    return {
      episodesApi: new EpisodesApiService(),
      episodes: []
    };
  },
  async created() {
    try {
      this.episodes = await this.episodesApi.getEpisodes();
    } catch (e) {
      console.error("Error al cargar episodios:", e);
    }
  }
});
</script>
```

---


