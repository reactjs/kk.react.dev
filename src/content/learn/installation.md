---
title: Орнату
---

<Intro>

React басынан бастап біртіндеп бейімделуді ескере отырып құрастырылған. Өз қажетінше cіз тек қажет React функциясын ғана пайдалана аласыз. Бұл бөлімдегі ақпарат React-пен алғаш танысқанда да, қарапайым динамикалық HTML бетін жасағанда немесе күрделі React қосымшасын жобалау кезінде де пайдалы.

</Intro>

<YouWillLearn isChapter={true}>

* [Жаңа React жобасын қалай бастау керек](/learn/start-a-new-react-project)
* [Бар жобаға React-тi қалай қосуға болады](/learn/add-react-to-an-existing-project)
* [Код редакторынызды қалай баптауға болады](/learn/editor-setup)
* [React Developer Tools құралын орнату жолы](/learn/react-developer-tools)

</YouWillLearn>

## React-тi қолданып көрy {/*try-react*/}

React-тi қолданып көру үшін ештеңе орнатудың қажеті жоқ. Құмжәшігте кодты өңдеңіз!

<Sandpack>

```js
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>;
}

export default function App() {
  return <Greeting name="world" />
}
```

</Sandpack>

Дәл осы жерде код жазуға немесе жоғарғы оң жақ бұрыштағы «Fork» түймесін басу арқылы кодты жаңа табта ашуға болады.

Most pages in the React documentation contain sandboxes like this. Outside of the React documentation, there are many online sandboxes that support React: for example, [CodeSandbox](https://codesandbox.io/s/new), [StackBlitz](https://stackblitz.com/fork/react), or [CodePen.](https://codepen.io/pen?template=QWYVwWN)

### Локальде React-тi қолданып көріңіз {/*try-react-locally*/}

Локальде компьютерінізде React-пен жұмыс жасап көру үшін осы [HTML бетін жүктеп алыңыз](https://gist.githubusercontent.com/gaearon/0275b1e1518599bbeafcde4722e79ed1/raw/db72dcbf3384ee1708c4a07d3be79860db04bff0/example.html). Оны редакторда және браузерде ашыңыз!

## Жаңа React жобасын бастаңыз {/*start-a-new-react-project*/}

Егер сіз React көмегімен қосымшаны немесе веб-сайтты толығымен құрғыныз келсе, [жаңа React жобасын бастаңыз.](/learn/start-a-new-react-project)

## React қосымшасын нөлден құру {/*build-a-react-app-from-scratch*/}

Егер фреймворк сіздің жобаңызға сәйкес келмесе, өз фреймворкіңізді құрғыныз келсе немесе React қосымшасының негіздерін үйренгіңіз келсе, [React қосымшасын нөлден құра аласыз.](/learn/build-a-react-app-from-scratch)

## Бар жобаға React-тi қосыңыз {/*add-react-to-an-existing-project*/}

Егер бұрыннан бар қосымшада немесе веб-сайтта React қолданып көргіңіз келсе, [бар жобаға React-ті қосыңыз.](/learn/add-react-to-an-existing-project)

<Note>

#### Create React App қолдану керек пе? {/*should-i-use-create-react-app*/}

Жоқ. Create React App ескірген. Қосымша ақпарат үшін [Create React App-тің тоқтатылуы](/blog/2025/02/14/sunsetting-create-react-app) бөлімін қараңыз.

</Note>

## Келесі қадамдар {/*next-steps*/}

Күнделікті кездесетін ең маңызды ұғымдармен танысу үшін [Жылдам бастау](/learn) бөліміне өтіңіз.

