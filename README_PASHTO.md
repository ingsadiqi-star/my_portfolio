# Rayan Jan — React Portfolio

دا یو Responsive، Dark Cinematic Portfolio دی چې په React او Vite جوړ شوی.

## ۱. د پروژې چلول

1. په کمپیوټر کې Node.js نصب کړه: https://nodejs.org/
2. دا ZIP فایل Extract کړه.
3. د پروژې فولډر په VS Code کې خلاص کړه.
4. په VS Code کې Terminal خلاص کړه او دا کمانډونه په ترتیب اجرا کړه:

```bash
npm install
npm run dev
```

5. Terminal کې ښکاره شوی محلي لینک (اکثره `http://localhost:5173`) په براوزر کې خلاص کړه.

## ۲. خپل معلومات بدلول

د `src/App.jsx` فایل په سر کې دا درې ارزښتونه بدل کړه:

```js
const GITHUB_URL = 'https://github.com/YOUR-USERNAME'
const LINKEDIN_URL = 'https://www.linkedin.com/in/YOUR-PROFILE'
const CONTACT_EMAIL = 'your-real-email@example.com'
```

- د `projects` په لېست کې د هرې پروژې `repo` لینک د هغې د اصلي GitHub repository لینک ته واړوه.
- د پروژو نومونه، توضیحات، ټکنالوژۍ او عکسونه د خپلو حقیقي پروژو مطابق بدل کړه.
- د مهارتونو لېست هم په `src/App.jsx` کې شته.
- د عکسونو اوسني لینکونه نمونه/illustrative دي؛ د خپلو پروژو screenshotونه وکاروه.

## ۳. د Contact Form مهم وضاحت

اوسنۍ فورمه د لیدونکي د ایمیل اپلیکیشن د خلاصولو لپاره `mailto:` کاروي؛ پیغام په خپله سرور ته نه لېږي. د حقیقي website-based message delivery لپاره د Formspree یا بل form backend حساب جوړ کړه او فورمه ورسره وصل کړه. خپل ایمیل په کوډ کې بدلول مه هېروه.

## ۴. GitHub ته پورته کول

1. په GitHub کې نوی repository جوړ کړه، مثلاً `rayan-jan-portfolio`.
2. د پروژې فولډر کې Terminal خلاص کړه او دا کمانډونه اجرا کړه:

```bash
git init
git add .
git commit -m "Create Rayan Jan portfolio"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/rayan-jan-portfolio.git
git push -u origin main
```

`YOUR-USERNAME` په خپل GitHub username بدل کړه. که Git د نوم او ایمیل غوښتنه وکړي، د خپل GitHub حساب مطابق یې تنظیم کړه.

## ۵. د GitHub Pages له لارې آنلاین خپرول

دا پروژه د Vite build ته اړتیا لري؛ یوازې د React source فایلونه د GitHub Pages په ساده upload سره نه چلېږي.

**اسانه لاره: GitHub Actions**

1. په GitHub کې repository خلاص کړه.
2. Settings → Pages ته لاړ شه.
3. Build and deployment کې **GitHub Actions** وټاکه.
4. په repository کې `.github/workflows/deploy.yml` فایل جوړ کړه (لاندې محتوا).
5. فایل commit او push کړه. د Actions tab کې deployment بشپړېدو ته انتظار وباسه؛ Pages URL به په Settings → Pages کې ښکاره شي.

### `.github/workflows/deploy.yml`

```yaml
name: Deploy portfolio to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - name: Install dependencies
        run: npm ci
      - name: Build
        run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

**یادونه:** `npm ci` د `package-lock.json` فایل ته اړتیا لري. د لومړي ځل لپاره په خپل کمپیوټر کې `npm install` اجرا کړه او تولید شوی `package-lock.json` هم GitHub ته upload کړه.

## د فولډر جوړښت

```text
rayan-jan-portfolio/
├── index.html
├── package.json
├── vite.config.js
├── .gitignore
├── README_PASHTO.md
└── src/
    ├── App.jsx
    ├── main.jsx
    └── styles.css
```


## د پروفایل عکس
ستاسې ورکړل شوی عکس په `public/images/rayan-profile.png` کې ځای پر ځای شوی او د اصلي Hero عکس په توګه کارول کېږي. که یې بدلول غواړې، نوی عکس هم په همدې نوم واچوه.
