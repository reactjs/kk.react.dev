---
title: React Developer Tools
---

<Intro>

React [компоненттерін](/learn/your-first-component) тексеру, [пропстар](/learn/passing-props-to-a-component) және [күй](/learn/state-a) өңдеу үшін React Developer Tools-ты пайдаланыңыз және өнімділік мәселелерін анықтаныз.

</Intro>

<YouWillLearn>

* React Developer Tools орнату жолы

</YouWillLearn>

## Браузер кеңейтімдері {/*browser-extension*/}

React көмегімен жасалған веб-сайттарды жөндеудің ең оңай жолы - React Developer Tools браузер кеңейтімін орнату. Ол бірнеше танымал браузерлер үшін қол жетімді:

* [**Chrome** үшін орнату](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
* [**Firefox** үшін орнату](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
* [**Edge** үшін орнату](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

Енді **React арқылы жасалған** веб-сайтқа кірсеңіз, _Components_ және _Profiler_ панельдерін көресіз.

![React Developer Tools extension](/images/docs/react-devtools-extension.png)

### Safari және басқа браузерлер {/*safari-and-other-browsers*/}
Басқа браузерлерге (мысалы Safari) орнату үшін npm [`react-devtools`](https://www.npmjs.com/package/react-devtools) пакеті арқылы: 
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```
Содан кейін терминалда келесі команданы шақырыныз:
```bash
react-devtools
```
Веб-сайтыңыздың `<head>` бөлігіне `<script>` тегін қосыңыз:
```html {3}
<html>
  <head>
    <script src="http://localhost:8097"></script>
```

Браузер құралдарында көру үшін веб-сайтыңызды қайта ашыныз.

![React Developer Tools standalone](/images/docs/react-devtools-standalone.png)

## Мобильдік қосымша (React Native) {/*mobile-react-native*/}
React Developer Tools [React Native](https://reactnative.dev/) көмегімен жасалған қосымшаларды зеттеу үшін қолдануға болады.

React Developer Tools пайдаланудың ең оңай жолы - оны жалпы деңгейде орнату:
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```
Содан кейін терминалда келесі команданы шақырыныз:
```bash
react-devtools
```
Ол іске қосылған кезде локальді React Native қосымшанызға қосылуы керек.

> Программа зерттеу құралдары бірнеше секундтан кейін қосылмаса, қолданбаны қайта жүктеп көріңіз.

[React Native дебаггингі туралы көбірек білу.](https://reactnative.dev/docs/debugging)
