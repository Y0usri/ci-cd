# 🚀 Exercice CI/CD – GitHub Actions

### BTS SIO SLAM – Pipeline CI avec tests automatisés

---

## 📌 Description

Cet exercice permet de découvrir la **CI (Intégration Continue)** grâce à GitHub Actions.
L’objectif est de lancer automatiquement un test à chaque **push** ou **pull request** sur GitHub.

🎯 **But :** vérifier la qualité du code avant validation
🧪 **Méthode :** exécuter automatiquement un test Node.js
📈 **Résultat attendu :**

* 🟢 pipeline vert → tests valides
* 🔴 pipeline rouge → tests échoués

---

## 📁 Structure du projet

```
exercice-ci-cd-2/
├── package.json
├── isEven.js
├── test.js
└── .github/
    └── workflows/
        └── ci.yml
```

---

## 🧠 Fonction à tester

```js
function isEven(number) {
  return number % 2 === 0;
}
module.exports = { isEven };
```

---

## 🧪 Test automatisé

```js
const { isEven } = require("./isEven");

const result = isEven(4);

if (result === true) {
  console.log("✔ Test réussi : 4 est bien pair");
  process.exit(0);
} else {
  console.error("❌ Test échoué : fonction incorrecte");
  process.exit(1);
}
```

---

## ⚙ Workflow GitHub Actions (`.github/workflows/ci.yml`)

```yml
name: CI Exercice 2

on: [push, pull_request]

jobs:
  test_job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

---

## 🛠 Installation locale

```
npm install
npm test
```

Résultat attendu :

✔ **Test réussi : 4 est bien pair**

---

## 🚀 Envoi sur GitHub

```
git init
git add .
git commit -m "Exercice CI/CD isEven"
git branch -M main
git remote add origin https://github.com/TON_COMPTE/TON_REPO.git
git push -u origin main
```

Ensuite :

1. Aller dans **Actions**
2. Observer le workflow exécuté automatiquement
3. Le badge (si ajouté dans le README) indique :

* 🟢 **passing** si tout fonctionne
* 🔴 **failing** si un test échoue

---

## 🔧 Exercice pratique à réaliser

### 🎯 Objectif

Faire échouer volontairement le pipeline, puis le faire repasser au vert.

---

### Étape 1 — Mettre le pipeline au ROUGE

Dans `test.js`, remplace :

```js
const result = isEven(4);
```

par :

```js
const result = isEven(5);
```

Puis :

```
npm test
git add .
git commit -m "Test KO volontaire"
git push
```

👉 **Le pipeline devient 🔴 et le badge passe en failing**

---

### Étape 2 — Repasse au VERT

Corrige le code ou le test, puis :

```
git add .
git commit -m "correction test"
git push
```

👉 **Le badge redevient 🟢 et le pipeline repasse au vert**

---

## 🎓 Compétences travaillées

| Compétence           | Objectif                                   |
| -------------------- | ------------------------------------------ |
| CI/CD                | Mise en place d’un workflow GitHub Actions |
| Qualité logicielle   | Tests automatisés                          |
| DevOps               | Automatisation du processus                |
| Travail collaboratif | Empêche le merge de code cassé             |

---

## 🎉 Conclusion

Vous avez mis en place :

✔ un projet Node.js
✔ un test automatisé
✔ un workflow CI
✔ un badge de statut dynamique

💼 **C’est la base de la qualité logicielle en entreprise.**
