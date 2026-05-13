# Frontend Mentor - Tip calculator app solution

This is a solution to the [Tip calculator app challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/tip-calculator-app-ugJNGbJUX). The project is implemented with Vue 3 and includes responsive layout behavior, interactive states, and full tip-per-person calculations.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
  - [AI Collaboration](#ai-collaboration)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Install dependencies](#install-dependencies)
  - [Run locally](#run-locally)
  - [Build for production](#build-for-production)
  - [Lint](#lint)
- [Screenshot workflow](#screenshot-workflow)
- [Deployment](#deployment)
  - [Deploy on Netlify](#deploy-on-netlify)
  - [Deploy on Vercel](#deploy-on-vercel)
- [Project structure](#project-structure)
- [Author](#author)
- [Acknowledgments](#acknowledgments)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the app depending on their device's screen size
- See hover states for all interactive elements on the page
- Calculate the correct tip and total cost of the bill per person

### Screenshot

If you want to include a screenshot later, add it at the project root (for example `screenshot.jpg`) and update this section:

```md
![Tip calculator preview](./screenshot.jpg)
```

For a complete step-by-step flow, see the [Screenshot workflow](#screenshot-workflow) section below.

### Links

- Solution URL: [Add your Frontend Mentor solution URL here](https://www.frontendmentor.io/)
- Live Site URL: [Add your deployed site URL here](https://your-live-site-url.com)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- Flexbox
- CSS Grid
- Mobile-first responsive workflow
- [Vue 3](https://vuejs.org/) (Options API)
- [Vue CLI](https://cli.vuejs.org/)

### What I learned

This project reinforced a few practical frontend patterns:

- Using Vue computed properties to keep derived values (`tipPerPerson`, `totalPerPerson`) centralized and reactive.
- Handling mutually exclusive user input patterns (preset tip buttons vs. custom tip input).
- Keeping validation feedback simple and immediate (people field zero-state error).
- Building a clean responsive card layout that adapts from desktop two-column to mobile one-column.

Example of a computed guard used in the app:

```js
tipPerPerson() {
  if (this.parsedBill === 0 || this.parsedPeople === 0) {
    return '0.00'
  }

  const tipAmount = this.parsedBill * (this.activeTipPercent / 100)
  return (tipAmount / this.parsedPeople).toFixed(2)
}
```

### Continued development

Areas to improve in future iterations:

- Add keyboard-first accessibility refinements and stronger focus styles.
- Support locale-aware currency formatting.
- Add unit tests for calculation logic and edge cases.
- Provide optional dark/light theme switching.

### Useful resources

- [Vue.js Documentation](https://vuejs.org/guide/introduction.html) - Helped with computed property and event-handling patterns.
- [Frontend Mentor Community](https://www.frontendmentor.io/) - Useful reference for challenge expectations and implementation comparisons.
- [MDN Web Docs](https://developer.mozilla.org/) - Helpful for CSS layout and form input behavior details.

### AI Collaboration

AI was used during this project to speed up implementation and polish:

- Assisted with scaffolding component structure and styling direction.
- Helped refine calculation logic and input validation behavior.
- Helped format and document the project with this README.

What worked well:

- Fast iteration on UI structure and responsive CSS.
- Quick sanity checks for edge cases.

What required manual review:

- Final UX decisions (spacing, colors, typography, and interaction details).
- Ensuring output matched the challenge requirements precisely.

## Getting started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm (comes with Node.js)

### Install dependencies

```bash
npm install
```

### Run locally

```bash
npm run serve
```

Then open the local URL shown in the terminal (typically `http://localhost:8080`).

### Build for production

```bash
npm run build
```

### Lint

```bash
npm run lint
```

## Screenshot workflow

Use this quick process to generate a clean `screenshot.jpg` for your README:

1. Start the app locally:

   ```bash
   npm run serve
   ```

2. Open the local URL (usually `http://localhost:8080`) in your browser.
3. Set a clean test state in the calculator (for example: bill `142.55`, tip `15%`, people `5`) so the result panel looks complete.
4. Take a screenshot:
   - **Windows:** `Win + Shift + S` (Snipping Tool)
   - **Browser option:** Right-click page and use built-in capture if available.
5. Save the image as `screenshot.jpg` in the project root:

   ```text
   tip-calc/screenshot.jpg
   ```

6. Confirm your README image path is:

   ```md
   ![Tip calculator preview](./screenshot.jpg)
   ```

## Deployment

### Deploy on Netlify

You can deploy this Vue CLI project on Netlify in a few minutes.

1. Push your project to GitHub.
2. Go to [Netlify](https://www.netlify.com/) and click **Add new site** → **Import an existing project**.
3. Connect your Git provider and select this repository.
4. Use these build settings:
   - **Build command:** `npm run build`
   - **Publish directory:** `dist`
5. Click **Deploy site**.
6. After deployment, copy the generated URL and place it in your README under `Live Site URL`.

### Deploy on Vercel

This project can also be deployed directly to Vercel.

1. Push your project to GitHub.
2. Go to [Vercel](https://vercel.com/) and click **Add New** → **Project**.
3. Import this repository.
4. Vercel usually detects Vue automatically. Verify these settings:
   - **Framework Preset:** `Vue.js`
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`
5. Click **Deploy**.
6. Copy your production URL and update the README `Live Site URL`.

Optional Vercel CLI deployment:

```bash
npm i -g vercel
vercel
```

Follow the prompts, then use the returned URL in your README links.

## Project structure

```text
tip-calc/
├─ public/
├─ src/
│  ├─ App.vue        # Tip calculator UI, logic, and styles
│  └─ main.js        # Vue app entry point
├─ README.md
└─ package.json
```

## Author

- Name - [Add your name here](https://www.your-site.com)
- Frontend Mentor - [@yourusername](https://www.frontendmentor.io/profile/yourusername)

## Acknowledgments

Thanks to Frontend Mentor for the challenge design and structured practice format.
