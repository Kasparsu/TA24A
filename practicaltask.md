# 🧪 Practical Task — Vue 3 Project with Bun, Vue Router & Bulma

**Level:** First year  
**Time estimate:** 60–90 minutes  
**Submission:** Push to GitHub — grader will clone and run `bun install && bun run dev`

> 📌 **This task is also a Git exercise.** You are expected to make small, focused commits at the checkpoints marked with 💾 throughout the task. The grader will read your commit history — it is part of the grade.

---

## 📖 Scenario

You are building a small multi-page colour showcase app. Each page fills the entire screen with a coloured card that displays the colour name. A navigation menu lets you switch between pages. The project uses Bun as the runtime and package manager, Vue 3 with Vue Router for the pages, and Bulma (installed via npm with Sass) for styling.

---

## ✅ Checklist Overview

- [ ] GitHub repository created and connected
- [ ] Vite + Vue 3 project scaffolded with Bun
- [ ] Vue Router installed and configured with 3 routes
- [ ] Navigation menu visible on all pages
- [ ] 3 pages — each a full-width, full-height coloured card showing the colour name
- [ ] Bulma installed via npm with Sass
- [ ] At least 6 atomic commits with meaningful messages pushed to GitHub

---

## 🔧 Part 1 — Repository Setup

### 1.1 — Create the GitHub repository

1. Go to [github.com](https://github.com) → **New repository**
2. Name it `colour-showcase`
3. Set to **Public**
4. Do **not** add a README, .gitignore, or licence — you will generate these yourself
5. Click **Create repository** and copy the HTTPS URL

---

### 1.2 — Scaffold the Vite + Vue project with Bun

Make sure Bun is installed:

```bash
bun --version
```

If not installed:

```bash
winget install Oven-sh.Bun
```

Open a terminal in the folder where you keep your projects and scaffold a new Vite project:

```bash
bun create vite colour-showcase --template vue
cd colour-showcase
```

Install the base dependencies:

```bash
bun install
```

Verify the dev server starts:

```bash
bun run dev
```

Open the URL shown in the terminal (`http://localhost:5173`) — you should see the default Vite + Vue page. Press `Ctrl+C` to stop it.

---

### 1.3 — Connect to GitHub

Initialise Git and push the scaffolded project:

```bash
git init
git add .
git commit -m "Scaffold Vite Vue project with Bun"
git remote add origin https://github.com/your-username/colour-showcase.git
git push -u origin main
```

> 💾 **Commit checkpoint 1 of 6** — your first commit is the scaffolded project as Vite generated it, nothing more.

---

## 💡 What Is an Atomic Commit?

Before continuing, read this — it applies to every commit you make for the rest of the task.

An **atomic commit** contains exactly **one logical change**. Not "I worked on stuff for an hour", not "all my files", and not one file per commit just because. One *idea* per commit.

**The test:** if you had to describe the commit in one short imperative sentence without using "and", it is probably atomic. If you find yourself writing "Add router and pages and styles and fix nav", you have four commits waiting to be separated.

**Why it matters in practice:**
- If something breaks, you can `git revert` the exact commit that caused it — without undoing unrelated work
- Your teammates (and your future self) can read the log and understand *what changed when and why*
- Interviewers look at commit history — a clean log signals a professional

**What atomic does NOT mean:**
- One file per commit — a single feature often touches multiple files, and that is fine
- Tiny to the point of uselessness — `"Fix typo in variable name"` is atomic; `"Change a"` is not
- Never combining related changes — `"Add RedPage, BluePage, GreenPage"` is one logical change (all three colour pages) and belongs in one commit

**Commit message rules (recap):**
- Imperative mood: `"Add"`, `"Fix"`, `"Remove"`, `"Update"` — not `"Added"` or `"Adding"`
- Under 72 characters on the subject line
- No trailing period
- If you need to explain *why*, add a blank line and a body

**Good examples for this task:**

| ✅ Good | ❌ Bad |
|--------|--------|
| `Scaffold Vite Vue project with Bun` | `initial commit` |
| `Add vue-router, bulma and sass dependencies` | `dependencies` |
| `Set up Bulma with Sass and global viewport reset` | `styles` |
| `Configure Vue Router with three colour page routes` | `router done` |
| `Add navbar with RouterLink navigation` | `app.vue` |
| `Add red, blue and green full-screen colour pages` | `pages` |

---

## 📦 Part 2 — Install Dependencies

### 2.1 — Install Vue Router

```bash
bun add vue-router
```

### 2.2 — Install Bulma and Sass

```bash
bun add bulma
bun add --dev sass
```

Verify `package.json` now lists all three as dependencies.

Commit the updated lockfile and package.json:

```bash
git add package.json bun.lockb
git commit -m "Add vue-router, bulma and sass dependencies"
git push
```

> 💾 **Commit checkpoint 2 of 6** — only `package.json` and `bun.lockb` change here. Nothing else. This commit is purely about adding dependencies.

---

## 🗂️ Part 3 — Project Structure

Before writing code, set up the folder structure. Delete the default boilerplate files you won't need:

- Delete `src/components/HelloWorld.vue`
- Delete `src/assets/vue.svg`
- Empty the contents of `src/style.css` (or delete it — you will replace it with Sass)
- Clear out `src/App.vue` — you will rewrite it

Your `src/` folder should look like this when you are done:

```
src/
├── assets/
│   └── main.scss        ← you will create this
├── pages/
│   ├── RedPage.vue      ← you will create this
│   ├── BluePage.vue     ← you will create this
│   └── GreenPage.vue    ← you will create this
├── router/
│   └── index.js         ← you will create this
├── App.vue              ← you will rewrite this
└── main.js              ← you will update this
```

Create the folders now:

```bash
mkdir src/pages
mkdir src/router
```

Commit the cleaned-up structure:

```bash
git add .
git commit -m "Remove Vite boilerplate and set up pages and router folders"
git push
```

> 💾 **Commit checkpoint 3 of 6** — deleting the default `HelloWorld.vue`, `vue.svg`, and clearing `App.vue` is one logical change: removing boilerplate. Commit it before writing any new code.

---

## 🎨 Part 4 — Sass & Bulma Setup

### 4.1 — Create the main Sass file

Create `src/assets/main.scss` and import Bulma:

```scss
@use "bulma/sass" as *;

// Make the app fill the full viewport
html,
body,
#app {
  height: 100%;
  margin: 0;
  padding: 0;
}
```

### 4.2 — Update `main.js` to use the Sass file

Open `src/main.js`. It currently imports `style.css` — replace that import with your new Sass file, and also add the router (which you will set up next):

```js
import { createApp } from 'vue'
import './assets/main.scss'
import App from './App.vue'
import { router } from './router/index.js'

createApp(App).use(router).mount('#app')
```

Commit the Sass setup:

```bash
git add src/assets/main.scss src/main.js
git commit -m "Set up Bulma with Sass and global viewport reset"
git push
```

> 💾 **Commit checkpoint 4 of 6** — `main.scss` (Bulma import + reset) and the updated `main.js` import together form one logical unit: "Bulma is now wired in." Note that only two files are staged — not everything with `git add .`. Stage what belongs to this change, nothing else.

---

## 🗺️ Part 5 — Vue Router

### 5.1 — Create the router

Create `src/router/index.js`:

```js
import { createRouter, createWebHashHistory } from 'vue-router'

import RedPage from '../pages/RedPage.vue'
import BluePage from '../pages/BluePage.vue'
import GreenPage from '../pages/GreenPage.vue'

const routes = [
  { path: '/',      component: RedPage,   name: 'Red'   },
  { path: '/blue',  component: BluePage,  name: 'Blue'  },
  { path: '/green', component: GreenPage, name: 'Green' },
]

export const router = createRouter({
  history: createWebHashHistory(),
  routes,
})
```

> 💡 `createWebHashHistory` is used here so the app works correctly when opened directly from the filesystem or GitHub Pages without any server-side routing config.

---

## 🧭 Part 6 — App.vue with Navigation

Rewrite `src/App.vue` to contain the Bulma navbar and a `<RouterView />` that fills the remaining space:

```vue
<script setup>
import { RouterView, RouterLink } from 'vue-router'
</script>

<template>
  <nav class="navbar is-dark" role="navigation">
    <div class="navbar-brand">
      <span class="navbar-item has-text-weight-bold">🎨 Colour Showcase</span>
    </div>

    <div class="navbar-menu is-active">
      <div class="navbar-start">
        <RouterLink class="navbar-item" to="/">Red</RouterLink>
        <RouterLink class="navbar-item" to="/blue">Blue</RouterLink>
        <RouterLink class="navbar-item" to="/green">Green</RouterLink>
      </div>
    </div>
  </nav>

  <RouterView />
</template>

<style scoped>
.navbar {
  position: sticky;
  top: 0;
  z-index: 10;
}
</style>
```

Commit the router and navbar together — they are one logical unit (the routing system is not useful without a nav, and the nav has nowhere to link without a router):

```bash
git add src/router/index.js src/App.vue
git commit -m "Configure Vue Router and add Bulma navbar with three links"
git push
```

> 💾 **Commit checkpoint 5 of 6** — `router/index.js` and `App.vue` together make navigation work. They belong in the same commit because neither is useful without the other. This is what "one logical change" means — it is not always one file.

---

## 📄 Part 7 — The Three Pages

Each page should fill the full width and height of the viewport (below the navbar) with a coloured card. The card displays the colour name in large, centred text.

### 7.1 — Red Page

Create `src/pages/RedPage.vue`:

```vue
<template>
  <section class="colour-page has-background-danger">
    <div class="colour-card card">
      <div class="card-content">
        <p class="title has-text-white has-text-centered">Red</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.colour-page {
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 52px); /* full height minus navbar */
  width: 100%;
}

.colour-card {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  box-shadow: none;
}

.title {
  font-size: 15vw;
  font-weight: 900;
  letter-spacing: 0.05em;
  text-shadow: 0 4px 24px rgba(0, 0, 0, 0.25);
}
</style>
```

### 7.2 — Blue Page

Create `src/pages/BluePage.vue`:

```vue
<template>
  <section class="colour-page has-background-info">
    <div class="colour-card card">
      <div class="card-content">
        <p class="title has-text-white has-text-centered">Blue</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.colour-page {
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 52px);
  width: 100%;
}

.colour-card {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  box-shadow: none;
}

.title {
  font-size: 15vw;
  font-weight: 900;
  letter-spacing: 0.05em;
  text-shadow: 0 4px 24px rgba(0, 0, 0, 0.25);
}
</style>
```

### 7.3 — Green Page

Create `src/pages/GreenPage.vue`:

```vue
<template>
  <section class="colour-page has-background-success">
    <div class="colour-card card">
      <div class="card-content">
        <p class="title has-text-white has-text-centered">Green</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.colour-page {
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 52px);
  width: 100%;
}

.colour-card {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
  box-shadow: none;
}

.title {
  font-size: 15vw;
  font-weight: 900;
  letter-spacing: 0.05em;
  text-shadow: 0 4px 24px rgba(0, 0, 0, 0.25);
}
</style>
```

---

## ▶️ Part 8 — Commit the Pages, Then Run & Verify

### 8.1 — Commit the three pages

All three colour pages are one logical unit — they implement the same feature together. Commit them as one atomic commit:

```bash
git add src/pages/
git commit -m "Add red, blue and green full-screen colour pages"
git push
```

> 💾 **Commit checkpoint 6 of 6** — three files, one commit. All three pages serve the same purpose and were added together. Splitting them into three separate commits (`"Add red page"`, `"Add blue page"`, `"Add green page"`) would be unnecessarily granular — each one is not useful in isolation.

---

### 8.2 — Verify your commit history

Before running the app, check your log looks clean:

```bash
git log --oneline
```

You should see something like:

```
a3f91c2 Add red, blue and green full-screen colour pages
b82d4e1 Configure Vue Router and add Bulma navbar with three links
c14a903 Set up Bulma with Sass and global viewport reset
d47f210 Remove Vite boilerplate and set up pages and router folders
e93b5c0 Add vue-router, bulma and sass dependencies
f28a1d7 Scaffold Vite Vue project with Bun
```

Six commits. Each one tells a clear story. A person who has never seen your project can read this log and understand exactly what was built and in what order — without opening a single file.

If yours says `"asdf"`, `"test"`, `"fix"`, `"wip"`, `"changes"` — fix it now with `git commit --amend` (for the last commit) or `git rebase -i` (for earlier ones) before pushing.

---

### 8.3 — Run the app and verify it works

```bash
bun run dev
```

Open `http://localhost:5173` and check:

- [ ] The dark navbar appears at the top with three links: Red, Blue, Green
- [ ] Clicking **Red** shows a full-screen red background with "Red" in large white text
- [ ] Clicking **Blue** shows a full-screen blue background with "Blue" in large white text
- [ ] Clicking **Green** shows a full-screen green background with "Green" in large white text
- [ ] Navigating between pages does not reload — Vue Router handles it client-side
- [ ] No errors in the browser console (press `F12` to check)

---

## ✅ Part 9 — Final GitHub Verification

Open your repository on GitHub and confirm:

- All 6 commits are visible under the **Commits** tab
- Each commit message is clear and in imperative mood
- The files `src/pages/RedPage.vue`, `src/pages/BluePage.vue`, `src/pages/GreenPage.vue`, `src/router/index.js`, `src/assets/main.scss` are all present
- `bun.lockb` is committed (not in `.gitignore`)
- The repository is **Public**

Click on individual commits on GitHub and read through them. The diff for each commit should show only the changes that belong to that commit's stated purpose — nothing more, nothing less.

---

## 🎯 Bonus Challenges

Completed the main task and want to go further? Try one or more of these:

**Bonus 1 — Active nav link styling**
Bulma's `is-active` class on a `navbar-item` highlights it. Vue Router automatically adds `router-link-active` class to matching links. Wire them up:

```vue
<RouterLink class="navbar-item" active-class="is-active" to="/">Red</RouterLink>
```

**Bonus 2 — Add a fourth colour page**
Add a new page of your own choice — pick any Bulma colour class (`has-background-warning`, `has-background-primary`, `has-background-link`) or use a custom hex colour with inline style. Add it to the router and the nav.

**Bonus 3 — Custom Bulma colour via Sass**
In `main.scss`, override a Bulma variable before importing Bulma to customise the colour palette:

```scss
@use "sass:color";

$danger: hsl(348, 86%, 43%);   // darker red

@use "bulma/sass" as *;
```

**Bonus 4 — Page transition animation**
Wrap `<RouterView />` in a Vue `<Transition>` component to add a fade effect when navigating between pages:

```vue
<RouterView v-slot="{ Component }">
  <Transition name="fade" mode="out-in">
    <component :is="Component" />
  </Transition>
</RouterView>
```

Add to your Sass file:

```scss
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```

---

## 📐 Grading Criteria

| Criteria | What the grader checks |
|----------|----------------------|
| Repository is Public on GitHub | Can be cloned without login |
| `bun install && bun run dev` works | No errors, app loads in browser |
| Vue Router configured with 3 routes | All three paths work (`/`, `/blue`, `/green`) |
| Navigation menu present on all pages | Navbar visible and links work |
| Each page is full width and height | No whitespace around the colour area |
| Each page shows the colour name | Text is visible, centred, and readable |
| Bulma used for styling | `has-background-*` classes used, Bulma imported via Sass |
| At least 6 atomic commits | Each commit covers one logical change — verified by reading the diff |
| Commit messages are meaningful | Imperative mood, under 72 chars, no "fix", "update", "stuff", "asdf" |
| No unrelated files mixed in commits | `git add .` was not used blindly — each commit stages only relevant files |

---

## 💡 Common Mistakes & Fixes

**The page background does not fill the full height**
Make sure `html, body, #app { height: 100% }` is in your `main.scss`. Without this, percentage heights on child elements have nothing to measure against.

**Bulma styles are not loading**
Check that `main.js` imports `./assets/main.scss` and that `main.scss` imports Bulma with `@use "bulma/sass" as *`. Make sure `sass` is installed as a dev dependency.

**Vue Router links cause a full page reload**
You are probably using a regular `<a href>` tag instead of `<RouterLink>`. Replace all navigation links with `<RouterLink to="...">`.

**White gap above or below the colour section**
The browser adds default margin to `body`. Ensure `margin: 0; padding: 0` is set on `html` and `body` in `main.scss`.

**`bun.lockb` is missing from the commit**
The lockfile must be committed so the grader gets exactly the same package versions when they run `bun install`. Run `git add bun.lockb` and commit it.

**The app shows a blank page**
Open the browser console (`F12`). If you see an error like `Failed to resolve import`, check the file paths in your `router/index.js` imports — they must match the actual filenames exactly, including capitalisation.

**"I used `git add .` everywhere and now my commits have random files in them"**
Check what you are about to stage before committing with `git status` and `git diff --staged`. If you already committed the wrong files, fix the last commit with:
```bash
git reset HEAD~1          # undo the commit, keep the files
git add only-the-right-files
git commit -m "Correct message"
```

**"I wrote bad commit messages and already pushed"**
For the last commit only (if you are the only one working on this):
```bash
git commit --amend -m "Better message here"
git push --force-with-lease
```
For earlier commits, use `git rebase -i` to reword them. Do this before submitting.

**"All my work is in one giant commit"**
If you forgot to commit at each checkpoint and now have one massive `git add . && git commit -m "everything"`, use `git reset HEAD~1` to undo it (your files are kept), then re-stage and commit in the correct atomic chunks.
