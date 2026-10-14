# Story Of 10 — Beginner Setup Guide

यह एक **frontend starter project** है। इसमें Home page, Hindi/Odia/English UI text, category filter, search, favorites, video modal, PWA files और local demo Admin form शामिल हैं।

## 1) फाइलें
- `index.html` — वेबसाइट Home
- `styles.css` — डिजाइन और responsive layout
- `app.js` — कहानियाँ, भाषा, सर्च, पसंदीदा और video player
- `admin.html` / `admin.js` — demo admin form
- `manifest.webmanifest` / `sw.js` — PWA starter
- `privacy.html` — privacy policy template

## 2) अपने कंप्यूटर पर टेस्ट करें
सबसे आसान: VS Code में project folder खोलें और Live Server extension से `index.html` चलाएँ।
या Python मौजूद हो तो terminal में project folder के अंदर:
`python -m http.server 8000`
फिर browser में `http://localhost:8000` खोलें।

सीधे `file://` से खोलने पर service worker/PWA काम नहीं करेगा। PWA के लिए HTTPS hosting चाहिए।

## 3) अपने वीडियो कैसे जोड़ें
1. वीडियो को ऐसी hosting/storage पर upload करें जो MP4 playback और पर्याप्त bandwidth सपोर्ट करती हो।
2. HTTPS video URL कॉपी करें।
3. `admin.html` खोलें, कहानी की जानकारी और URL भरें, फिर Save Story दबाएँ।
4. Home page पर लौटें और video चलाकर टेस्ट करें।

**महत्वपूर्ण:** इस starter का Admin data `localStorage` में रहता है। इसका अर्थ है कि कहानी उसी browser/device में दिखेगी जहाँ उसे जोड़ा गया है। यह real shared admin/database नहीं है। Public launch से पहले Firebase/secure backend और protected admin authentication जोड़ें। इस demo Admin को public site पर अकेला छोड़ना सुरक्षित नहीं है।

## 4) Domain और hosting पर publish करना
1. अपने बजट के अनुसार domain registrar से domain खरीदें (जैसे उपलब्ध होने पर `storyof10.in`)।
2. Static hosting provider पर account बनाकर project files deploy करें। GitHub Pages, Cloudflare Pages या Netlify जैसे विकल्पों के current free-plan limits जाँचें।
3. Hosting dashboard में domain जोड़ें और registrar में दिए गए DNS records ठीक वैसे ही सेट करें।
4. HTTPS certificate active होने तक प्रतीक्षा करें।
5. `https://yourdomain/` और `https://yourdomain/admin.html` जाँचें।
6. Privacy policy में असली contact email, data practices और effective date भरें।

## 5) Android app में बदलना — Capacitor का रास्ता
वेबसाइट को पहले HTTPS पर चलाएँ और production build/URL तय करें। Android app बनाने के लिए Node.js LTS और Android Studio install करें। Terminal में project folder के लिए:

```bash
npm init -y
npm install @capacitor/core @capacitor/cli
npm install @capacitor/android
npx cap init "Story Of 10" "com.storyof10.app" --web-dir=.
npx cap add android
npx cap sync android
npx cap open android
```

Capacitor के लिए local web asset configuration अपने installed Capacitor version के हिसाब से जाँचें। Static site में `index.html` web root पर है, इसलिए `webDir` उसी folder को इंगित करे; यदि Capacitor project अलग बनाया है, website files को उसके configured webDir में रखें। फिर Android Studio में Gradle sync करें और Run दबाएँ।

Production app के लिए navigation, back button, network errors, status bar, app icon, privacy disclosures, permissions और video playback का परीक्षण करें। सिर्फ WebView wrapper होने से Play Store approval की गारंटी नहीं है; ऐप में पर्याप्त उपयोगिता और Play policies का पालन जरूरी है।

## 6) Ads
- Website: AdSense या उपयुक्त ad network के लिए आवेदन करें; approval की गारंटी नहीं है। Privacy policy, original content, consent और ad-network rules पूरे करें।
- Android: AdMob SDK/ads बाद में जोड़ें। पहले test ad units का इस्तेमाल करें, live ads पर खुद क्लिक न करें।
- विज्ञापन और privacy requirements देश, audience (विशेषकर बच्चों) और platform के अनुसार बदल सकते हैं।

## 7) Public launch से पहले जरूरी काम
- Demo Admin को secure करें या हटाएँ।
- Shared cloud database + admin authentication जोड़ें।
- Video storage/streaming budget तय करें और bandwidth limits जाँचें।
- Favorites को account/cloud storage या device persistence के साथ लागू करें।
- असली privacy policy, contact page, content rights और report/takedown process तैयार करें।
- वेबसाइट और Android app पर अलग-अलग फोन/ब्राउज़र में टेस्ट करें।
