<template>
  <div
    class="container-center q-px-xl full-width text-left"
    style="max-width: 1350px; margin: 0 auto"
  >
    <div class="flex items-center q-mb-md reveal-projects">
      <h3 class="text-h3 text-weight-bold text-white q-my-none">Projets</h3>
    </div>
    <p class="text-grey-5 text-h6 text-weight-light q-mb-xl max-width-text reveal-projects">
      Une vitrine de mes travaux récents, mettant en valeur mon expérience.
    </p>

    <div class="flex q-gutter-sm q-mb-xl reveal-projects" style="flex-wrap: wrap">
      <q-btn
        v-for="cat in categories"
        :key="cat"
        unelevated
        no-caps
        :label="cat"
        @click="currentCategory = cat"
        :class="[currentCategory === cat ? 'btn-filter-active' : 'btn-filter-inactive', 'q-mb-sm']"
      />
    </div>

    <div class="row q-col-gutter-xl items-stretch">
      <div
        v-for="project in filteredProjects"
        :key="project.id"
        class="col-12 col-sm-6 col-md-4 reveal-projects"
      >
        <q-card
          class="project-card bg-card-dark no-shadow overflow-hidden full-height flex column"
          :style="{ '--brand-color': project.brandColor }"
        >
          <div class="image-wrapper relative-position">
            <q-img :src="project.image" class="project-image full-height" fit="cover">
              <template v-slot:error>
                <div class="absolute-full flex flex-center bg-grey-9 text-white">
                  Image indisponible
                </div>
              </template>
            </q-img>
            <div class="gradient-overlay absolute-full"></div>
          </div>

          <q-card-section class="col-grow flex column q-pa-lg">
            <div class="title-container flex justify-between items-start q-mb-sm">
              <div class="text-h6 text-white text-weight-bold project-title-transition title-text">
                {{ project.title }}
              </div>
              <div class="text-caption text-grey-6 font-mono q-pt-xs">{{ project.year }}</div>
            </div>

            <p
              class="text-grey-5 text-body2 q-mb-md ellipsis-3-lines line-height-relaxed description-fixed-height"
            >
              {{ project.description }}
            </p>

            <q-space />
            <div class="flex q-gutter-xs q-mb-sm tags-container">
              <q-chip
                v-for="tech in project.technologies"
                :key="tech"
                dense
                :ripple="false"
                class="chip-tech-da no-margin"
              >
                {{ tech }}
              </q-chip>
            </div>
          </q-card-section>

          <q-card-actions class="q-pa-lg q-pt-none q-gutter-sm row">
            <div class="col">
              <q-btn
                outline
                no-caps
                label="Détails"
                class="full-width btn-action-outline"
                @click="openDetails(project)"
              />
            </div>
            <div class="col" v-if="project.liveLink">
              <q-btn
                outline
                no-caps
                label="View Live"
                icon-right="launch"
                class="full-width btn-action-outline"
                :href="project.liveLink"
                target="_blank"
              />
            </div>
            <div class="col" v-if="project.repoLink && !project.liveLink">
              <q-btn
                outline
                no-caps
                label="Code"
                icon-right="code"
                class="full-width btn-action-outline"
                :href="project.repoLink"
                target="_blank"
              />
            </div>
          </q-card-actions>
        </q-card>
      </div>
    </div>

    <q-dialog v-model="detailsOpen" backdrop-filter="blur(8px) brightness(30%)">
      <q-card class="modal-dark-tech text-white" style="width: 1100px; max-width: 95vw">
        <q-card-section class="row items-center q-pa-lg bg-header-modal">
          <div class="text-h5 text-weight-bold">{{ selectedProject?.title }}</div>
          <q-space />
          <q-btn icon="close" flat round dense v-close-popup class="text-grey-5" />
        </q-card-section>

        <q-separator dark />

        <q-card-section class="q-pa-xl scroll modal-body-scroll">
          <div class="row q-col-gutter-xl">
            <div class="col-12 col-md-7 text-center">
              <q-img
                :src="selectedProject?.image"
                class="rounded-borders shadow-24 border-glass"
                :ratio="16 / 9"
              >
                <template v-slot:error>
                  <div class="absolute-full flex flex-center bg-grey-9 text-white">
                    Image indisponible
                  </div>
                </template>
              </q-img>
              <div class="q-mt-lg flex q-gutter-sm justify-center">
                <q-btn
                  outline
                  color="white"
                  label="Live Demo"
                  icon="launch"
                  no-caps
                  class="rounded-borders"
                  v-if="selectedProject?.liveLink"
                  :href="selectedProject?.liveLink"
                  target="_blank"
                />
                <q-btn
                  outline
                  color="white"
                  label="Code"
                  icon="code"
                  no-caps
                  class="rounded-borders"
                  v-if="selectedProject?.repoLink"
                  :href="selectedProject?.repoLink"
                  target="_blank"
                />
              </div>
            </div>

            <div class="col-12 col-md-5 flex column justify-center">
              <div class="q-mb-xl">
                <h6 class="text-subtitle1 text-weight-bold text-white flex items-center q-mb-md">
                  <q-icon name="work_outline" color="purple-4" size="xs" class="q-mr-sm" />
                  VALORISATION DE L'EXPÉRIENCE
                </h6>
                <div class="q-mb-md">
                  <div class="text-purple-3 text-weight-bold text-uppercase text-caption q-mb-xs">
                    Mon Rôle & Autonomie
                  </div>
                  <div class="text-body2 text-grey-4 line-height-relaxed">
                    {{ selectedProject?.role }}
                  </div>
                </div>
                <div class="q-mb-md">
                  <div class="text-purple-3 text-weight-bold text-uppercase text-caption q-mb-xs">
                    Interactions Équipe
                  </div>
                  <div class="text-body2 text-grey-4 line-height-relaxed">
                    {{ selectedProject?.interactions }}
                  </div>
                </div>
              </div>

              <q-separator dark class="q-mb-xl" />

              <div>
                <h6 class="text-subtitle1 text-weight-bold text-white flex items-center q-mb-md">
                  <q-icon name="psychology" color="purple-4" size="xs" class="q-mr-sm" />
                  ANALYSE RÉFLEXIVE
                </h6>
                <div
                  class="text-body2 text-grey-4 line-height-relaxed italic border-left-purple q-pl-md q-py-xs"
                >
                  "{{ selectedProject?.reflexive }}"
                </div>
              </div>
            </div>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted } from 'vue';
import { animate } from 'motion';

interface Project {
  id: number;
  title: string;
  category: string;
  description: string;
  image: string;
  year: number;
  technologies: string[];
  brandColor: string;
  role: string;
  interactions: string;
  reflexive: string;
  liveLink?: string;
  repoLink?: string;
}

const currentCategory = ref('All');
const categories = ['All', 'Web', 'Mobile', 'Logiciel', 'Machine Learning'];
const detailsOpen = ref(false);
const selectedProject = ref<Project | null>(null);

// Données
const projects = ref<Project[]>([
  {
    id: 1,
    title: 'Orion V2 - Gestion de Stock',
    category: 'Web',
    brandColor: '#A855F7',
    description:
      "Plateforme complète de gestion d'entrepôts et d'inventaires développée pour Misyl Services.",
    image: 'https://cdn.quasar.dev/img/parallax1.jpg',
    year: 2026,
    technologies: ['Vue.js', 'NestJS', 'PostgreSQL', 'Pinia','Docker','JavaScript','TypeScript'],
    role: "Développeur Full-Stack. Conception du modèle de données complexe et développement de l'API REST et des interfaces.",
    interactions:
      'Travail en binôme avec un autre stagiaire, nécessitant des compétences en communication et de la coordination.',
    reflexive:
      "Ce projet m'a appris à concevoir avant de coder et à prioriser la maintenabilité (Clean Architecture).",
  },
  {
    id: 2,
    title: 'Woopets - Application Mobile',
    category: 'Mobile',
    brandColor: '#A855F7',
    description:
      'Application mobile (iOS/Android) transposant le test en ligne "Quelle race de chien est faite pour vous ?".',
    image: 'https://cdn.quasar.dev/img/parallax2.jpg',
    year: 2025,
    technologies: ['React Native', 'TypeScript', 'Firebase', 'Expo'],
    role: "Développeur Mobile Front-End. Autonomie sur le choix de l'architecture React Native et la transposition de l'algorithme PHP en TS.",
    interactions: 'Travail en autonomie avec validations régulières auprès du tuteur de stage.',
    reflexive:
      "J'ai appris l'importance de l'expérience utilisateur (UX) sur mobile, et la gestion de la frustration face aux bugs spécifiques.",
    liveLink: 'https://www.woopets.fr/chien/test-race-de-chien/',
  },
  {
    id: 3,
    title: 'Campus Talk',
    category: 'Web',
    brandColor: '#A855F7',
    description:
      "Application web de réseau social permettant d'envoyer des messages, créer des fils et s'abonner.",
    image: 'img/campusTalk.png',
    year: 2024,
    technologies: ['Java', 'JEE', 'PostgreSQL', 'HTML/CSS'],
    role: "Développeur Full-Stack. Réalisation de l'API REST, gestion de la base de données et sécurisation (XSS, SQL Injection).",
    interactions:
      "Projet collaboratif universitaire (IUT). Répartition des tâches et suivi régulier de l'avancement.",
    reflexive:
      "J'ai renforcé ma compréhension des mécanismes de sécurité web fondamentaux et du fonctionnement des servlets Java.",
    repoLink: 'https://github.com/Nexiorr/CampusTalk',
  },
  {
    id: 4,
    title: 'Application de classification',
    category: 'Machine Learning',
    brandColor: '#A855F7',
    description:
      'Application permettant de charger (CSV), classifier et afficher un ensemble de données avec un algo KNN.',
    image: 'img/knn.png',
    year: 2024,
    technologies: ['Java', 'JavaFX', 'Algorithmique', 'Data'],
    role: "Développeur Java. Implémentation de l'algorithme K-Nearest Neighbors (KNN) et conception de l'interface JavaFX.",
    interactions:
      "Travail en groupe. Communication sur la structure des données partagées entre l'IHM et l'algorithme.",
    reflexive:
      "Ce projet m'a permis de faire le pont entre les mathématiques (distance euclidienne) et l'informatique visuelle (nuage de points).",
    repoLink: 'https://github.com/Nexiorr/Classification-knn',
  },
  {
    id: 5,
    title: 'FlyingDustries',
    category: 'Logiciel',
    brandColor: '#A855F7',
    description:
      "Application gérant une interface utilisateur et utilisant l'algorithme de Dijkstra pour calculer le chemin le plus court.",
    image: 'img/projetTrajet1.png',
    year: 2023,
    technologies: ['Java', 'JavaFX', 'Dijkstra'],
    role: "Développeur Java. Conception de l'interface JavaFX et intégration de l'algorithme de recherche de graphe.",
    interactions:
      'Projet de première année (IUT) réalisé en équipe avec utilisation de Git pour le versioning commun.',
    reflexive:
      "Première vraie confrontation avec la théorie des graphes appliquée à un cas d'usage visuel et interactif.",
    repoLink: 'https://github.com/Nexiorr/FlyingDustries',
  },
  {
    id: 6,
    title: 'Application de reservation',
    category: 'Web',
    brandColor: '#A855F7',
    description: 'Application web de reservation',
    image: 'img/reservation.png',
    year: 2025,
    technologies: ['Java', 'SpringBoot', 'PostgreSQL', 'Rest', 'Bootstrap', 'jsp'],
    role: "Développeur Java. Création d' une application de réservation, adaptable à différents contextes (hôtel, restaurant, etc.) avec gestion des disponibilités et des utilisateurs.",
    interactions:
      'Projet de troisième année (IUT) réalisé en binôme avec utilisation de Git pour le versioning commun',
    reflexive:
      "Mise en situation de la conception à la réalisation d'une application en respectant les demandes d'un client",
    repoLink: 'https://github.com/Nexiorr/app-reservation',
  },
  {
    id: 7,
    title: 'Émulateur de processeur Risc-V',
    category: 'Logiciel',
    brandColor: '#A855F7',
    description:
      'Un émulateur de processeur RISC-V en ligne de commande pour exécuter des programmes basiques compilés pour cette architecture.',
    image: 'img/rien',
    year: 2025,
    technologies: ['Rust', 'Terminal','Docker'],
    role: 'Développeur. Implémentation du jeu d\'instructions RISC-V de base et de la boucle d\'exécution du processeur virtuel.',
    interactions:
      'Projet en binôme',
    reflexive:
      "Compréhension approfondie de l'architecture matérielle et de l'exécution d'instructions bas niveau.",
    repoLink: '#',
  },
  {
    id: 8,
    title: 'Planetarium',
    category: 'Web',
    brandColor: '#A855F7',
    description:
      'Reproduction multijoueur du gameplay d\'Agar.io. Architecture client/serveur avec WebSocket. Les joueurs peuvent se déplacer, manger des cellules plus petites, grandir et entrer en collision. Gestion en temps réel de la position, de la taille, de la nourriture et du classement sur le serveur.',
    image: 'img/agarIjava.png',
    year: 2023,
    technologies: ['JavaScript', 'Node.js', 'WebSocket', 'Canvas API'],
    role: 'Développeur JavaScript. Implémentation du serveur WebSocket (connexions, déplacements, collisions) et de l\'affichage Canvas.',
    interactions:
      'Projet en équipe de 3. Coordination entre la logique Backend temps réel et le rendu Frontend.',
    reflexive:
      "Ce projet m'a confronté aux défis de la synchronisation de données en temps réel via sockets, des calculs de collisions côté serveur et de la mise à l'échelle visuelle d'un élément dans un Canvas sans recharger la page.",
    repoLink: '#',
  },
  {
    id: 9,
    title: 'NerdFactory',
    category: 'Logiciel',
    brandColor: '#A855F7',
    description:
      'Jeu simple sur terminal réalisé sous 3 jours dans une équipe utilisant la méthodologie Agile.',
    image: 'img/NerdFactory.png',
    year: 2023,
    technologies: ['Java', 'Terminal', 'Agile'],
    role: 'Développeur Java. Création des mécaniques de jeu en console.',
    interactions:
      'Mise en pratique concrète de la méthode Agile (Scrum) avec des sprints très courts.',
    reflexive:
      "J'ai appris l'importance de la communication quotidienne (Daily Scrum) pour éviter de coder la même fonctionnalité qu'un collègue.",
    repoLink: '#',
  },
]);

const filteredProjects = computed(() => {
  if (currentCategory.value === 'All') return projects.value;
  return projects.value.filter((p) => p.category.toLowerCase() === currentCategory.value.toLowerCase());
});

const openDetails = (project: Project) => {
  selectedProject.value = project;
  detailsOpen.value = true;
};

onMounted(() => {
  // Animation au scroll
  const observer = new IntersectionObserver(
    (entries) => {
      let delay = 0;
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          animate(
            entry.target,
            { opacity: [0, 1], y: [40, 0] },
            { delay: delay, duration: 0.8, ease: 'easeOut' },
          );
          delay += 0.2;
          observer.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.1 },
  );

  document.querySelectorAll('.reveal-projects').forEach((el) => {
    observer.observe(el);
  });
});
</script>

<style scoped>
/* ========================================================== */
/* ALIGNEMENT ET TYPOGRAPHIE                                  */
/* ========================================================== */
.max-width-text {
  max-width: 700px;
}
.line-height-relaxed {
  line-height: 1.6;
}

.reveal-projects {
  opacity: 0;
}

/* ========================================================== */
/* FILTRES (MINI-NAVBAR)                                      */
/* ========================================================== */
.btn-filter-active {
  background: #7c3aed !important;
  color: white !important;
  border-radius: 6px;
  font-weight: 500;
  padding: 4px 16px;
}
.btn-filter-inactive {
  background: rgba(255, 255, 255, 0.05) !important;
  color: #8a92a3 !important;
  border-radius: 6px;
  font-weight: 500;
  padding: 4px 16px;
  transition: all 0.3s ease;
}
.btn-filter-inactive:hover {
  background: rgba(255, 255, 255, 0.1) !important;
  color: #ffffff !important;
}

/* ========================================================== */
/* STYLE DES CARTES ET HOMOGÉNÉISATION DES HAUTEURS           */
/* ========================================================== */
.project-card {
  border-radius: 12px;
  background: #111111;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  height: 100%; /* S'assure que la carte prend toute la hauteur de la colonne */
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  border-color: rgba(124, 58, 237, 0.3);
}

/* Fixer la hauteur de l'image (environ équivalent au ratio 16/9 sur ces largeurs) */
.image-wrapper {
  height: 200px;
  min-height: 200px;
  overflow: hidden;
}

.gradient-overlay {
  background: linear-gradient(to top, #111111 0%, transparent 40%);
  pointer-events: none;
}

.project-image {
  transition: transform 0.5s ease;
  filter: brightness(0.9);
}
.project-card:hover .project-image {
  transform: scale(1.03);
  filter: brightness(1);
}

/* Fixer une hauteur min pour le titre pour gérer les titres sur 1 ou 2 lignes */
.title-container {
  min-height: 56px;
}
.title-text {
  line-height: 1.3;
}

/* Fixer une hauteur pour la description (3 lignes max) */
.description-fixed-height {
  height: 66px; /* Ajuste selon ton line-height, ici 3 lignes * 1.6em */
  margin-bottom: 16px;
}

/* Fixer une hauteur pour le conteneur de tags */
.tags-container {
  min-height: 28px; /* Hauteur d'une rangée de chips */
}

/* Le highlight du titre au survol */
.project-card:hover .project-title-transition {
  color: #a855f7 !important;
}
.project-title-transition {
  transition: color 0.3s ease;
}

/* ========================================================== */
/* LABELS EXACTEMENT COMME LE SCREEN                          */
/* ========================================================== */
.chip-tech-da {
  background: rgba(124, 58, 237, 0.12) !important;
  color: #a78bfa !important;
  border-radius: 16px;
  font-weight: 500;
  padding: 2px 14px;
  font-size: 12px;
}

/* ========================================================== */
/* BOUTONS ACTIONS (OUTLINED)                                 */
/* ========================================================== */
.btn-action-outline {
  border: 1px solid rgba(255, 255, 255, 0.15) !important;
  color: #e2e8f0 !important;
  border-radius: 6px;
  font-weight: 500;
  height: 40px;
  transition: all 0.3s ease;
}
.btn-action-outline:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(255, 255, 255, 0.4) !important;
}

/* ========================================================== */
/* MODALE DARK TECH                                           */
/* ========================================================== */
.modal-dark-tech {
  background: #0b0e14 !important;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 20px !important;
}
.bg-header-modal {
  background: rgba(255, 255, 255, 0.02);
}
.modal-body-scroll {
  max-height: 75vh;
}
.border-left-purple {
  border-left: 3px solid #7c3aed;
}
.border-glass {
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.ellipsis-3-lines {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
