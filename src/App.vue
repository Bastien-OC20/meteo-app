<template>
  <section class="container">
    <div class="overlay-icone-chargement">
      <img
        src="./assets/ressources/chargement/circles.svg"
        alt="logo chargement"
      />
    </div>
    <h1>Application météo</h1>

    <CurrentDay />
    <PrevisionDay />
    <CurrentHours />
    <div></div>
  </section>
</template>

<script>
import CurrentDay from "./components/CurrentDay.vue";
import PrevisionDay from "./components/PrevisionDay.vue";
import CurrentHours from "./components/CurrentHours.vue";

export default {
  name: "App",
  components: {
    CurrentDay,
    PrevisionDay,
    CurrentHours,
  },
  data() {
    return {};
  },

  mounted() {
    const CLEFAPI = "379a51582fe63ed2ee09a821404e11ad";
    let resultatsAPI;

    const temps = document.querySelector(".temps");
    const temperature = document.querySelector(".temperature");
    const localisation = document.querySelector(".localisation");
    const heure = document.querySelectorAll(".heure-nom-prevision");
    const tempPourH = document.querySelectorAll(".heure-prevision-valeur");
    const joursDiv = document.querySelectorAll(".jour-prevision-nom");
    const tempJoursDiv = document.querySelectorAll(".jour-prevision-temp");
    const imgIcone = document.querySelectorAll(".logo-meteo");
    const chargementContainer = document.querySelector(
      ".overlay-icone-chargement"
    );

    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          console.log(position);
          let long = position.coords.longitude;
          let lat = position.coords.latitude;
          AppelAPI(long, lat);
        },
        () => {
          alert(
            `Vous avez refusé la géolocalisation, l'application ne peur pas fonctionner, veuillez l'activer.!`
          );
        }
      );
    }
    function AppelAPI(long, lat) {
      fetch(
        `https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${long}&exclude=minutely&units=metric&lang=fr&appid=${CLEFAPI}`
      )
        .then((reponse) => {
          return reponse.json();
        })
        .then((data) => {
          console.log(data);

          resultatsAPI = data;

          temps.innerText = resultatsAPI.current.weather[0].description;
          temperature.innerText = `${Math.trunc(resultatsAPI.current.temp)}°`;
          localisation.innerText = resultatsAPI.timezone;

          // les heures, par tranche de trois, avec leur temperature.

          let heureActuelle = new Date().getHours();

          for (let i = 0; i < heure.length; i++) {
            let heureIncr = heureActuelle + i * 3;

            if (heureIncr > 24) {
              heure[i].innerText = `${heureIncr - 24} h`;
            } else if (heureIncr === 24) {
              heure[i].innerText = "00 h";
            } else {
              heure[i].innerText = `${heureIncr} h`;
            }
          }

          // temp pour 3h
          for (let j = 0; j < tempPourH.length; j++) {
            tempPourH[j].innerText = `${Math.trunc(
              resultatsAPI.hourly[j * 3].temp
            )}°`;
          }

          // trois premieres lettres des jours

          for (let k = 0; k < tabJoursEnOrdre.length; k++) {
            joursDiv[k].innerText = tabJoursEnOrdre[k].slice(0, 3);
          }

          // Temps par jour
          for (let m = 0; m < 7; m++) {
            tempJoursDiv[m].innerText = `${Math.trunc(
              resultatsAPI.daily[m + 1].temp.day
            )}°`;
          }

          // Icone dynamique
          if (heureActuelle >= 6 && heureActuelle < 21) {
            imgIcone.src =
              "../assets/ressources/jour/${resultatsAPI.current.weather.icon}.svg";
          } else {
            imgIcone.src =
              "../assets/ressources/nuit/${resultatsAPI.current.weather.icon}.svg";
          }

          chargementContainer.classList.add("disparition");
        });
    }

    const joursSemaine = [
      "Lundi",
      "Mardi",
      "Mercredi",
      "Jeudi",
      "Vendredi",
      "Samedi",
      "Dimanche",
    ];

    let ajd = new Date();
    let options = { weekday: "long" };
    let jourActuel = ajd.toLocaleDateString("fr-FR", options);
    console.log(jourActuel, ajd);

    jourActuel = jourActuel.charAt(0).toUpperCase() + jourActuel.slice(1);

    let tabJoursEnOrdre = joursSemaine
      .slice(joursSemaine.indexOf(jourActuel))
      .concat(joursSemaine.slice(0, joursSemaine.indexOf(jourActuel)));
    console.log(tabJoursEnOrdre);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

*,
::before,
::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
*,
::before,
::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  color: #f1f1f1;
  background: linear-gradient(45deg, #868686, rgb(22, 28, 29));
  height: 100vh;
}

.container {
  display: flex;
  flex-direction: column;
  width: 60%;
  margin: auto;
  background: linear-gradient(45deg, #1068b6, #ecea60);
  border: 3px solid #f1f1f1;
  border-radius: 30px;
}

h1 {
  display: flex;
  justify-content: center;
  align-items: center;
  border-bottom: 1.5px solid #f1f1f1;
  padding: 3%;
  margin-bottom: 2%;
  font-size: 2em;
}

/* Animation chargement */

.overlay-icone-chargement {
  position: absolute;
  left: 15%;
  top: 5%;
  width: 70%;
  height: 100%;
  background: linear-gradient(45deg, #868686, #161c1d);
  transition: opacity 1.1s ease-out;
  z-index: 1000;
}
.overlay-icone-chargement img {
  width: 150px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.disparition {
  opacity: 0;
}
</style>
