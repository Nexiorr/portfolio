<template>
  <div
    class="container-center q-px-xl full-width text-left"
    style="max-width: 1200px; margin: 0 auto"
  >
    <div class="flex items-center q-mb-xl reveal-exp">
      <h3 class="text-h3 text-weight-bold text-white q-my-none">Expérience Professionnelle</h3>
    </div>

    <div class="row q-col-gutter-xl">
      <div class="col-12" v-for="(exp, index) in experiences" :key="exp.id">
        <q-card
          class="experience-card bg-transparent no-shadow reveal-exp"
          :class="{ 'q-mt-xl': index > 0 }"
        >
          <q-card-section class="q-pa-none">
            <!-- En-tête de l'expérience -->
            <div class="row items-center q-mb-md">
              <div class="col-12 col-md-8">
                <h4 class="text-h4 text-weight-bold text-white q-mb-xs">{{ exp.role }}</h4>
                <div class="text-h6 text-purple-4 text-weight-medium">
                  {{ exp.company }}
                  <span class="text-grey-5 text-body1 q-ml-sm">• {{ exp.period }}</span>
                </div>
              </div>
            </div>

            <q-separator dark class="q-my-md opacity-20" />

            <div class="row q-col-gutter-xl q-mt-md">
              <!-- Colonne de gauche : Contexte & Missions -->
              <div class="col-12 col-md-6">
                <div class="q-mb-lg">
                  <h5 class="text-h6 text-white text-weight-bold flex items-center q-mb-sm">
                    <q-icon name="business" color="purple-4" size="sm" class="q-mr-sm" />
                    Contexte & Entreprise
                  </h5>
                  <p class="text-grey-4 text-body1 line-height-relaxed">{{ exp.context }}</p>
                </div>

                <div class="q-mb-lg">
                  <h5 class="text-h6 text-white text-weight-bold flex items-center q-mb-sm">
                    <q-icon name="task_alt" color="purple-4" size="sm" class="q-mr-sm" />
                    Missions Confiées
                  </h5>
                  <ul class="text-grey-4 text-body1 line-height-relaxed custom-list">
                    <li v-for="(mission, mIdx) in exp.missions" :key="mIdx">{{ mission }}</li>
                  </ul>

                  <div class="q-mt-md">
                    <div class="text-purple-3 text-weight-bold text-caption text-uppercase q-mb-xs">
                      Stack Technique
                    </div>
                    <div class="flex q-gutter-xs flex-wrap">
                      <q-chip
                        v-for="tech in exp.stack"
                        :key="tech"
                        dense
                        :ripple="false"
                        class="chip-tech-da no-margin"
                      >
                        {{ tech }}
                      </q-chip>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Colonne de droite : Autonomie & Interactions -->
              <div class="col-12 col-md-6">
                <div class="q-mb-lg">
                  <h5 class="text-h6 text-white text-weight-bold flex items-center q-mb-sm">
                    <q-icon name="explore" color="purple-4" size="sm" class="q-mr-sm" />
                    Degré d'Autonomie
                  </h5>
                  <p class="text-grey-4 text-body1 line-height-relaxed">{{ exp.autonomy }}</p>
                </div>

                <div class="q-mb-lg">
                  <h5 class="text-h6 text-white text-weight-bold flex items-center q-mb-sm">
                    <q-icon name="diversity_3" color="purple-4" size="sm" class="q-mr-sm" />
                    Interactions
                  </h5>
                  <ul class="text-grey-4 text-body1 line-height-relaxed custom-list">
                    <li v-for="(interaction, iIdx) in exp.interactions" :key="iIdx">
                      {{ interaction }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>

            <!-- Analyse Réflexive (Point 5 du CDC) -->
            <div class="reflexive-box q-mt-lg q-pa-lg rounded-borders">
              <h5 class="text-h6 text-white text-weight-bold flex items-center q-mb-md">
                <q-icon name="psychology_alt" color="purple-3" size="sm" class="q-mr-sm" />
                Analyse Réflexive : Connaissance & Conscience de Soi
              </h5>

              <div class="row q-col-gutter-md">
                <div class="col-12 col-sm-6">
                  <div class="text-purple-3 text-weight-bold text-caption text-uppercase q-mb-xs">
                    Ce que j'ai appris sur moi-même
                  </div>
                  <p class="text-grey-4 text-body2 line-height-relaxed">
                    {{ exp.reflexiveAnalysis.learned }}
                  </p>
                </div>
                <div class="col-12 col-sm-6">
                  <div class="text-purple-3 text-weight-bold text-caption text-uppercase q-mb-xs">
                    Mes points forts identifiés
                  </div>
                  <p class="text-grey-4 text-body2 line-height-relaxed">
                    {{ exp.reflexiveAnalysis.strengths }}
                  </p>
                </div>
                <div class="col-12 col-sm-6">
                  <div class="text-purple-3 text-weight-bold text-caption text-uppercase q-mb-xs">
                    Mes axes de progrès
                  </div>
                  <p class="text-grey-4 text-body2 line-height-relaxed">
                    {{ exp.reflexiveAnalysis.improvements }}
                  </p>
                </div>
                <div class="col-12 col-sm-6">
                  <div class="text-purple-3 text-weight-bold text-caption text-uppercase q-mb-xs">
                    Mes besoins pour évoluer
                  </div>
                  <p class="text-grey-4 text-body2 line-height-relaxed">
                    {{ exp.reflexiveAnalysis.needs }}
                  </p>
                </div>
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue';
import { animate } from 'motion';

interface ReflexiveAnalysis {
  learned: string;
  strengths: string;
  improvements: string;
  needs: string;
}

interface Experience {
  id: string;
  role: string;
  company: string;
  period: string;
  context: string;
  missions: string[];
  stack: string[];
  autonomy: string;
  interactions: string[];
  reflexiveAnalysis: ReflexiveAnalysis;
}

const experiences: Experience[] = [
  {
    id: '1',
    role: 'Stagiaire Développeur Full-Stack',
    company: 'Misyl Services (Projet Orion)',
    period: 'Stage BUT Mars 2026 - Juillet 2026',
    context:
      "Misyl Services est une ESN française qui possède un outil centralisant un ensemble d'applications utilisé par les internes de la société (Orion V1). Le projet consistait à externaliser la brique « Gestion de Stock » vers Orion V2.",
    missions: [
      "Conception de l'architecture Backend (entités, services) en NestJS avec base de données PostgreSQL.",
      "Développement de l'interface Frontend complète de gestion des entrepôts, emplacements et racks (Vue.js / Quasar).",
      "Implémentation d'une fonctionnalité d'autocomplétion d'adresses en s'appuyant sur l'API du gouvernement français.",
      "Développement de la logique métier de l'inventaire virtuel (Products et Packagings) et refactoring constant (Clean Code).",
    ],
    stack: ['Vue.js', 'Quasar', 'Pinia', 'NestJS', 'TypeORM', 'PostgreSQL', 'Docker'],
    autonomy:
      "Responsabilité partagée de l'architecture : développement de la logique métier (Back) et de la gestion d'état (Front) en forte autonomie, avec des revues de code régulières pour assurer la maintenabilité.",
    interactions: [
      "Travail en binôme étroit avec un autre stagiaire : répartition des tâches (UI vs logique métier/connexion) et synchronisation via l'API Gateway.",
      "Réunions internes de conception fonctionnelle et d'architecture avec l'équipe projet.",
      'Séances de refactoring conjointes pour séparer proprement la logique métier des vues.',
    ],
    reflexiveAnalysis: {
      learned:
        "J'ai pris conscience de l'importance vitale du 'Clean Code' et de la séparation des responsabilités. Un code fonctionnel n'est pas suffisant s'il n'est pas maintenable par l'équipe.",
      strengths:
        'Mon adaptabilité pour monter en compétence rapidement sur des frameworks complets (NestJS, Vue 3, Quasar) et ma vision globale (Full-Stack).',
      improvements:
        "Au début, j'avais tendance à inclure de la logique métier directement dans les composants front-end. Je dois continuer à systématiser l'externalisation des fonctions.",
      needs:
        "Je souhaite continuer à évoluer dans des équipes qui pratiquent rigoureusement les Code Reviews, afin d'affiner mon expertise architecturale.",
    },
  },
  {
    id: '2',
    role: 'Stagiaire Développeur Mobile',
    company: 'Digistart (projet Woopets)',
    period: 'Stage BUT Avril 2026 - Juin 2026',
    context:
      "Digistart est l'entreprise éditrice de Woopets, un site web spécialisé sur les animaux de compagnie. L'objectif global de ce stage était de concevoir et développer une application mobile dédiée, transposant le test web existant « Quelle race de chien est faite pour vous ? » afin d'améliorer l'accessibilité et l'engagement utilisateur.",
    missions: [
      'Transposition du questionnaire web vers un format mobile ergonomique (iOS/Android).',
      "Adaptation d'un algorithme de tri (initialement en PHP) en TypeScript pour le traitement des résultats de compatibilité côté client.",
      "Développement de l'interface permettant d'afficher instantanément les recommandations avec des fiches détaillées de races.",
      "Tests de validation et préparation de l'application pour un déploiement sur les plateformes (App Store, Google Play).",
    ],
    stack: ['React Native', 'TypeScript', 'Firebase', 'Expo'],
    autonomy:
      "Très forte autonomie sur la réalisation technique (notamment le choix de React Native et l'adaptation de l'algorithme) tout en respectant strictement le cahier des charges fonctionnel et le design fourni.",
    interactions: [
      'Travail en équipe: Points de synchronisation et validation des étapes clés avec le tuteur de stage et le chef de projet.',
      "Recherche et partage: Recherche d'informations techniques de manière indépendante pour pallier aux problématiques de transposition web -> mobile.",
      "Documentation du code pour assurer l'exploitation et la maintenance future par l'équipe interne.",
    ],
    reflexiveAnalysis: {
      learned:
        "J'ai découvert ma capacité à m'approprier un code existant (l'algorithme PHP) pour le comprendre en profondeur et le repenser totalement dans un autre paradigme (TypeScript/Mobile).",
      strengths:
        "Ma persévérance face aux problèmes bloquants (ex: adaptation de la base de données). Ma capacité à toujours garder en tête l'expérience de l'utilisateur final.",
      improvements:
        "Apprendre à solliciter de l'aide et des conseils plus rapidement au lieu de rester bloqué trop longtemps sur un détail technique.",
      needs:
        'Évoluer dans un environnement avec des développeurs plus expérimentés (Code Review, Pair Programming) pour continuer à acquérir des bonnes pratiques et des standards architecturaux.',
    },
  },
];

onMounted(() => {
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

  document.querySelectorAll('.reveal-exp').forEach((el) => {
    observer.observe(el);
  });
});
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

.reveal-exp {
  opacity: 0;
}

.experience-card {
  border-left: 2px solid rgba(124, 58, 237, 0.3);
  padding-left: 32px;
  position: relative;
}

.experience-card::before {
  content: '';
  position: absolute;
  left: -9px;
  top: 0;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #7c3aed;
  box-shadow: 0 0 10px #7c3aed, 0 0 0 0 rgba(124, 58, 237, 0.4);
  animation: pulse-dot 2s infinite cubic-bezier(0.66, 0, 0, 1);
}

@keyframes pulse-dot {
  0% { box-shadow: 0 0 0 0 rgba(124, 58, 237, 0.4); }
  70% { box-shadow: 0 0 0 12px rgba(124, 58, 237, 0); }
  100% { box-shadow: 0 0 0 0 rgba(124, 58, 237, 0); }
}

.line-height-relaxed {
  line-height: 1.7;
}

.opacity-20 {
  opacity: 0.2;
}

.custom-list {
  padding-left: 20px;
  margin: 0;
}

.custom-list li {
  margin-bottom: 8px;
}

.custom-list li::marker {
  color: #a78bfa;
}

.reflexive-box {
  background: rgba(124, 58, 237, 0.05);
  border: 1px solid rgba(124, 58, 237, 0.2);
  transition: all 0.3s ease;
}

.reflexive-box:hover {
  background: rgba(124, 58, 237, 0.08);
  border-color: rgba(124, 58, 237, 0.4);
}

.chip-tech-da {
  background: rgba(124, 58, 237, 0.12) !important;
  color: #a78bfa !important;
  border-radius: 16px;
  font-weight: 500;
  padding: 2px 14px;
  font-size: 12px;
}
</style>
