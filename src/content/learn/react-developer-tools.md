---
title: React Developer Tools
---

<Intro>

Use React Developer Tools to inspect React [components](/learn/your-first-component), edit [props](/learn/passing-props-to-a-component) and [state](/learn/state-a-components-memory), and identify performance problems.

</Intro>

<YouWillLearn>

* How to install React Developer Tools

</YouWillLearn>

## Browser extension {/*browser-extension*/}

The easiest way to debug websites built with React is to install the React Developer Tools browser extension. It is available for several popular browsers:

* [Install for **Chrome**](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
* [Install for **Firefox**](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)
* [Install for **Edge**](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil)

Now, if you visit a website **built with React,** you will see the _Components_ and _Profiler_ panels.

![React Developer Tools extension](/images/docs/react-devtools-extension.png)

### Safari and other browsers {/*safari-and-other-browsers*/}
For other browsers (for example, Safari), install the [`react-devtools`](https://www.npmjs.com/package/react-devtools) npm package:
```bash
# Yarn
yarn global add react-devtools

# Npm
npm install -g react-devtools
```

Next open the developer tools from the terminal:
```bash
react-devtools
```

Then connect your website by adding the following `<script>` tag to the beginning of your website's `<head>`:
```html {3}
<html>
  <head>
    <script src="http://localhost:8097"></script>
```

Reload your website in the browser now to view it in developer tools.

![React Developer Tools standalone](/images/docs/react-devtools-standalone.png)

## Мобильдік қосымша (React Native) {/*mobile-react-native*/}

[React Native](https://reactnative.dev/) көмегімен жасалған қосымшаларды тексеру үшін [React Native DevTools](https://reactnative.dev/docs/react-native-devtools) қолдана аласыз - бұл React Developer Tools-ты тереңінен біріктіретін кіріктірілген дебаггер. Барлық функциялар браузер кеңейтімімен бірдей жұмыс істейді, соның ішінде натив элементтерді бөлектеу және таңдау.

[React Native дебаггингі туралы көбірек білу.](https://reactnative.dev/docs/debugging)

> React Native 0.76-дан бұрынғы нұсқалары үшін жоғарыдағы [Safari және басқа браузерлер](#safari-and-other-browsers) нұсқаулығын ұстан отырып React DevTools-тың автономды нұсқасын қолданыңыз.
