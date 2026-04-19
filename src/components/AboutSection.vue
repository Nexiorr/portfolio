<template>
  <div class="content-wrapper q-px-xl full-width text-left" style="max-width: 1200px; margin: 0 auto;">

    <div class="flex items-center q-mb-xl reveal-about">
      <h3 class="text-h3 text-weight-bold text-white q-my-none">
        Positionnement Professionnel
      </h3>
    </div>

    <div class="row q-col-gutter-xl">

      <div class="col-12 col-md-6">

        <div class="q-mb-xl reveal-about">
          <h4 class="text-h5 text-weight-bold text-white q-mb-md flex items-center">
            <q-icon name="rocket_launch" color="purple-4" size="sm" class="q-mr-sm"/>
            Mon Profil
          </h4>
          <p class="text-grey-4 line-height-relaxed text-body1">
            Actuellement en fin de cycle (BUT Informatique), je me positionne comme un <strong>Développeur Full-Stack junior</strong>.
            Mon projet professionnel à court terme est d'intégrer une équipe agile où je pourrai consolider mon expertise
            sur des architectures robustes (Spring Boot / NestJS) et des interfaces modernes, tout en appliquant les bonnes pratiques.
          </p>
        </div>

        <div class="reveal-about">
          <div class="flex justify-between items-end q-mb-md">
            <h4 class="text-h5 text-weight-bold text-white q-my-none flex items-center">
              <q-icon name="laptop_mac" color="purple-4" size="sm" class="q-mr-sm"/>
              Expertise Technique
            </h4>
          </div>

          <p class="text-grey-5 text-body2 q-mb-lg italic">
            "Ma stack technique est le reflet des problématiques résolues en stage et en projet. Je privilégie toujours l'outil le plus adapté au besoin."
          </p>

          <div class="bento-grid">
            <div v-for="(category, index) in techStack" :key="index" class="skill-category">

            <div class="flex items-center q-mb-sm">
              <q-icon :name="category.icon" color="purple-3" size="sm" class="q-mr-sm" />
              <div class="text-subtitle1 text-white text-weight-bold">{{ category.title }}</div>
            </div>

            <p class="text-grey-5 text-caption q-mb-md line-height-relaxed">
              {{ category.context }}
            </p>

            <div v-for="(tech, tIndex) in category.skills" :key="tIndex" class="q-mb-sm">
              <div class="flex justify-between text-caption text-grey-3 q-mb-xs">
                <span>{{ tech.name }}</span>
              </div>
            </div>

            </div>
          </div>
        </div>

      </div>

      <div class="col-12 col-md-6 reveal-about">

        <h4 class="text-h5 text-weight-bold text-white q-mb-md flex items-center">
          <q-icon name="psychology" color="purple-4" size="sm" class="q-mr-sm"/>
          Compétences Comportementales
        </h4>

        <p class="text-grey-5 text-body2 q-mb-md">
          Au-delà du code, voici les compétences humaines que j'ai développées lors de mes expériences en entreprise et travaux de groupe.
        </p>

        <q-list dark bordered class="rounded-borders soft-skills-list bg-transparent">

          <q-expansion-item group="softskills" icon="accessibility_new" label="Adaptabilité & Résolution de problèmes" header-class="text-weight-medium text-white" expand-icon-class="text-purple-4">
            <q-card class="bg-transparent">
              <q-card-section class="text-grey-4 text-body2 line-height-relaxed">
                Passer d'un environnement Java strict à la souplesse de Node.js/Vue m'a appris à m'adapter rapidement. Face à un bug bloquant, j'adopte une démarche méthodique (lecture des logs, documentation) avant de solliciter l'équipe.
              </q-card-section>
            </q-card>
          </q-expansion-item>

          <q-expansion-item group="softskills" icon="forum" label="Communication : Écoute & Feedbacks" header-class="text-weight-medium text-white" expand-icon-class="text-purple-4">
            <q-card class="bg-transparent">
              <q-card-section class="text-grey-4 text-body2 line-height-relaxed">
                J'accorde une grande importance à la reformulation lors des briefs. Durant mes Code Reviews sur GitLab, j'ai appris à recevoir la critique technique non pas comme une attaque, mais comme une opportunité d'amélioration du code commun.
              </q-card-section>
            </q-card>
          </q-expansion-item>

          <q-expansion-item group="softskills" icon="groups" label="Collectif : Coopération & Initiative" header-class="text-weight-medium text-white" expand-icon-class="text-purple-4">
            <q-card class="bg-transparent">
              <q-card-section class="text-grey-4 text-body2 line-height-relaxed">
                Je ne conçois pas le développement comme une tâche isolée. Face à un choix d'architecture (ex: SQL vs NoSQL), je privilégie toujours l'argumentation basée sur les faits plutôt que sur l'opinion, favorisant ainsi un consensus sain en équipe.
              </q-card-section>
            </q-card>
          </q-expansion-item>

        </q-list>

      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import { animate } from 'motion'

interface TechSkill {
  name: string;
}

interface TechCategory {
  title: string;
  icon: string;
  context: string;
  skills: TechSkill[];
}

// =========================================================================
// DONNÉES DE LA STACK TECHNIQUE
// C'est ici que tu peux facilement modifier/ajouter tes technos !
// =========================================================================
const techStack = ref<TechCategory[]>([
  {
    title: 'Architecture Backend & API',
    icon: 'dns',
    context: 'Conception d\'API RESTful sécurisées et architectures scalables (Expérience en stage et BUT).',
    skills: [
      { name: 'Java (JEE, Spring Boot)' },
      { name: 'Node.js (NestJS, Express)'},
      { name: 'Bases (C, Python)' }
    ]
  },
  {
    title: 'Écosystème JS & Frontend',
    icon: 'web',
    context: 'Création d\'interfaces réactives, typage fort et développement cross-platform.',
    skills: [
      { name: 'JavaScript / TypeScript' },
      { name: 'Vue.js / Quasar' },
      { name: 'React / React Native' },
      { name: 'UI (Tailwind, JSP)' }
    ]
  },
  {
    title: 'Data, DevOps & Outils',
    icon: 'storage',
    context: 'Modélisation de données, conteneurisation et intégration continue.',
    skills: [
      { name: 'SQL (PostgreSQL, MySQL)' },
      { name: 'NoSQL (MongoDB, Firebase, Redis)' },
      { name: 'GitLab CI / Docker' }
    ]
  }
])

onMounted(() => {
  // Animation d'apparition au scroll pour la section "About"
  const observer = new IntersectionObserver((entries) => {
    let delay = 0;
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        animate(
          entry.target,
          { opacity: [0, 1], y: [40, 0] },
          { delay: delay, duration: 0.8, ease: "easeOut" }
        )
        delay += 0.2;
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.1 })

  document.querySelectorAll('.reveal-about').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<style scoped>
.section-badge {
  background: rgba(124, 58, 237, 0.15);
  color: #a78bfa;
  border: 1px solid rgba(124, 58, 237, 0.3);
  padding: 8px 18px;
  border-radius: 30px;
  display: inline-flex;
  align-items: center;
  font-size: 0.9rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.line-height-relaxed {
  line-height: 1.7;
}

.reveal-about {
  opacity: 0;
}

/* Grille Bento pour les compétences */
.bento-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}

/* Style des cartes de compétences */
.skill-category {
  /* On ajoute une bordure très fine et un fond semi-transparent */
  background: rgba(255, 255, 255, 0.01);
  border: 1px solid rgba(255, 255, 255, 0.03);
  border-left: 3px solid #7C3AED; /* Ta barre violette actuelle */

  padding: 16px 20px;
  border-radius: 4px 12px 12px 4px;

  /* Ombre portée très diffuse pour la profondeur */
  box-shadow: 0 10px 30px -15px rgba(0, 0, 0, 0.5);

  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.skill-category:hover {
  background: rgba(124, 58, 237, 0.04); /* Légère teinte violette au survol */
  transform: translateX(8px);
  border-color: rgba(124, 58, 237, 0.2);
}

/* Style des accordéons Soft Skills */
.soft-skills-list {
  border-color: rgba(255, 255, 255, 0.08);
  background: rgba(0,0,0,0.2) !important;
}
</style>
