---
title: React философиясы
---

<Intro>

React сіз жоспарлайтын жобалар мен құрастырған қосымшалар туралы қөзқарасынызды өзгерте алады. React көмегімен пайдаланушы интерфейсін құрастырған кезде алдымен оны *компонет* атты бөліктерге бөлесіз. Содан кейін сіз компоненттеріңіздің әрқайсысын әртүрлі визуалды күйлерді сипаттайсыз. Соңында, деректер олардың бойымен әрекеттесуі үшін компоненттерді біріктіресіз. Бұл нұсқауда біз React арқылы іздеуге болатын өнімдер кестесін жасау мысалын қарастырамыз.

</Intro>

## Макеттен бастайық {/*start-with-the-mockup*/}

Сізде JSON API және дизайнердің макеті бар деп елестетіп көріңіз.

JSON API келесідей деректерді қайтарады:

```json
[
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" }
]
```

Макет көрінісі мынадай:

<img src="/images/docs/s_thinking-in-react_ui.png" width="300" style={{margin: '0 auto'}} />

React қосымшасымен UI жасаған кезде әдетте бірдей бес қадамды орындайсыз.

## 1-қадам: UI құрамдас бөліктерге бөліңіз {/*step-1-break-the-ui-into-a-component-hierarchy*/}

Макетті әрбір компонент пен қосалқы компоненттерге іріктеп оларға атау беруден бастаңыз. Дизайнермен жұмыс жасасаңыз, олар дизайн құралында компоненттерді атаған болуы мүмкін. Олардан біліңіз!

Сіз өзіңіздің тәжірибеңізге байланысты дизайнды компонентерге бөлyге болытын жолдар:

<<<<<<< HEAD
* **Программалау**--қарапайым функцияны немесе объект жасау туралы шешім қабылдаған кездегі тәсілді қолданыңыз. Техниканың бірі [single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle), бір компонент бір тапсырманы орындауы тиіс. Егер функционал уақыт өте келе ұлғайса, оны кішірек ішкі құрамдастарға бөлу керек.
* **CSS**--ойлаңыз, неліктен класс селектірін жасайтындығыңызды. (Дегенмен компоненттер соншалықты кішірейтілмегенін есте сақтаңыз.)
* **Дизайн**--дизайн қабаттарын қалай ұйымдастыратыныңызды ойлаңыз.
=======
* **Programming**--use the same techniques for deciding if you should create a new function or object. One such technique is the [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns), that is, a component should ideally only be concerned with one thing. If it ends up growing, it should be decomposed into smaller subcomponents. 
* **CSS**--consider what you would make class selectors for. (However, components are a bit less granular.)
* **Design**--consider how you would organize the design's layers.
>>>>>>> d271a7ac11d2bf0d6e95ebdfacaf1038421f9be0

Егер сіздің JSON жақсы құрылымдалған болса, cіз оның UI компонент құрылымына табиғи түрде сәйкес келетінін жиі байқайсыз. Себебі UI және деректер үлгілері жиі бірдей ақпараттық архитектураға, яғни бірдей пішінге ие болады. Пайдаланушы интерфейсін компонентерге бөліңіз, олардың әрқайсысы деректер үлгісінің бір бөлігін көрсетеді.

Бұл экранда бес компонент бар:

<FullWidth>

<CodeDiagram flip>

<img src="/images/docs/s_thinking-in-react_ui_outline.png" width="500" style={{margin: '0 auto'}} />

1. `FilterableProductTable` (сұр) бүкіл қосымшаны қамтиды.
2. `SearchBar` (көк) пайдаланушы енгізуін қабылдайды.
3. `ProductTable` (лаванда) пайдаланушы енгізуіне сәйкес тізімді көрсетеді және фильтрлейди.
4. `ProductCategoryRow` (жасыл) санат тақырыптарын көрсетеді.
5. `ProductRow`	(сары) жеке өнімдерді көрсетеді.

</CodeDiagram>

</FullWidth>

Егер сіз `ProductTable` (лаванда) қарасаңыз, кесте тақырыбы ("Name" және "Price" белгілері бар) оның жеке компонент бөлігі емес екенін көресіз. Оны ажырату керек пе, жоқ па, бұл жеке таңдау. Бұл мысалда ол "ProductTable" бөлігі болып табылады, себебі ол "ProductTable" тізімінде. Дегенмен, болашақта тақырыпқа жаңа функционалдылықты қоссаңыз (мысалы, өнімдерді сұрыптау мүмкіндігі), оны оқшау `ProductTableHeader` құрамдас бөлігіне шығаруға болады.

Макеттегі компоненттерді анықтағаннан кейін, оларды иерархияға орналастырыңыз. Басқа компоненттердін бөлігі болып табылатын компонент бөліктер иерархияда еншілес болады:

* `FilterableProductTable`
    * `SearchBar`
    * `ProductTable`
        * `ProductCategoryRow`
        * `ProductRow`

## 2-қадам: React колдынып статикалық нұсқаны жасаңыз {/*step-2-build-a-static-version-in-react*/}

Енді барлық компонент бөліктер иерархиялық ретпен орналастырылғандықтан, қосымшаны жүзеге асыратын уақыт келді. Ең қарапайым жолы -- интерфейсті деректер үлгісімен толтырып ешбір интерактивті қоспай көрсететін нұсқаны құру... Алдымен статикалық нұсқаны құрастыру және интерактивті кейінірек қосу әдетте оңай. Статикалық қосымшаны жазу көп теруді және өте аз ойлауды қажет етеді, ал интерактивті қосу көп теруді емес, көп ойлауды қажет етеді.

Деректер үлгісін көрсететін компонент статикалық нұсқасын жасау үшін, бізге басқа компоненттерді қолданатын және мәліметтерді өткізетін [пропс](/learn/passing-props-to-a-component) [компоненттерді](/learn/your-first-component) жасау керекпіз. 

Пропс ұғынығы негізгі (parent) компоненттен еншілес (child) компонентке деректерді жіберу тәсілi.

(Күй ұғымымен таныс болсаңыз, бұл статикалық нұсқаны құру үшін [күйді](/learn/state-a-components-memory) қолданбаймыз. Күй тек интерактивтілік, яғни уақыт өте келе өзгеретін деректер үшін керек. Бұл жасап жатқан мысал қосымша статикалық нұсқа болғандықтан күй қажет емес.)

Компонент бөліктерді иерархияда жоғарырақ құрудан бастау арқылы "жоғарыдан төменге" ("FilterableProductTable") немесе төменгі компонентерден ("ProductRow") "төменнен жоғарыға" сияқты тәсілдер бар. Қарапайым қосымшаларда иерархияда жоғары компоненттердер бастаған ыңғайлы. Қарапайым мысалдарда жоғарыдан төменге жобалау оңай. Күрделі қосымшаларда алдымен төменгі компонентерден жасап бастау ыңғайлырақ.

<Sandpack>

```jsx src/App.js
function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar() {
  return (
    <form>
      <input type="text" placeholder="Search..." />
      <label>
        <input type="checkbox" />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

function FilterableProductTable({ products }) {
  return (
    <div>
      <SearchBar />
      <ProductTable products={products} />
    </div>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 10px;
}
td {
  padding: 2px;
  padding-right: 40px;
}
```

</Sandpack>
(Егер бұл код оңай емес болып көрінсе, алдымен [Жылдам бастауға](/learn/) өтіңіз!)

Компоненттерді құрастырғаннан кейін деректер үлгісін көрсететін қайта пайдалануға болатын компонент кітапханасы болады. Бұл статикалық қосымша болғандықтан, компоненттер тек JSX қайтарады. Иерархияның жоғарғы жағындағы компонент (`FilterableProductTable`) деректерді пропс ретінде қабылдайды. Бұл _бір жақты деректер ағыны_ деп аталады, себебі деректер жоғары деңгейлі компонент бөліктен ағаштың төменгі жағындағы компоненттерге қолжетімді.

<Pitfall>

Әзірге ешқандай күй мәндерін пайдаланбаймыз. Бұл келесі қадам үшін!

</Pitfall>

## 3-қадам: UI күйінің минималды, бірақ толық көрінісін анықтаңыз {/*step-3-find-the-minimal-but-complete-representation-of-ui-state*/}

UI-ды интерактивті ету үшін пайдаланушыларға негізгі деректер үлгісін өзгертуге рұқсат беру керек. Бұл үшін * күйді * пайдаланасыз.

Күй туралы айтқанда біздін қосымшамызда өзгеретін деректердің ең аз жиынтығын айтамыз. Оны құрудың ең бастысы - принципті [DRY (Don't Repeat Yourself).](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) Қосымшаңызға қажетті ең аз талап етілетін күйді анықтаңыз. Қалғанының қажетінше есептеңіз. Мысалы, сатып алу тізімін жасап жатсаңыз, элементтерді массив ретінде күйде сақтауға болады. Тізімдегі элементтердің санын көрсеткіңіз келсе, элементтер санын басқа күй мәні ретінде сақтамаңыз -- оның орнына массивіңіздің ұзындығын есептеніз.

Енді осы мысалдағы барлық деректер бөліктерін ойлап көріңіз:

1. Өнімдердің түпнұсқалық тізімі
2. Пайдаланушы енгізген іздеу мәтіні
3. Чекбокстың мәні
4. Өнімдердің фильтрленген тізімі

Бұлардың қайсысы күй eмесін анықтаңыз:

* Уақыт өте келе **өзгеріссіз** қала ма? Олай болса, бұл деректер күйде сақталмауы керек.
* Олар пропс арқылы негізгі **компоненттен берілді** ме? Олай болса, бұл деректер күйде сақталмауы керек.
* Оларды компоненттегі бар күйлерден немесе деректемелер негізінде **есептей аласыз ба**? Олай болса, бұл деректер *міндетті түрде* күйде сақталмауы керек!

Ал қалған деректер мүмкін күйде сақталуы керек.

Оларды тағы да қарастырайық:

1. Өнімдердің бастапқы тізімі **пропс ретінде берілген, сондықтан ол күй емес.**
2. Іздеу мәтіні күй болып көрінеді, өйткені ол уақыт өте өзгереді және ештеңеден есептелмейді.
3. Чекбокстың мәні күй болып көрінеді, себебі ол уақыт өте өзгереді және ештеңеден есептелмейді.
4. Өнімдердің фильтр тізімі **күй емес, өйткені оны есептеуге болады**, іздеу мен чекбокс мәнін пайдаланып тізімді реттейміз.

Тек іздеу мен чекбокс мәні күй екенін анықтап алдық! Керемет!

<DeepDive>

#### Пропс пен күйдің айырмашылығы {/*props-vs-state*/}

React-те «модельдік» деректердің екі түрі бар: пропс және күй. Олар бір-бірінен айырмашылықтары бар:

* [**Пропс** функцияға беретін аргументтер сияқты.](/learn/passing-props-to-a-component) Олар негізгі компоненттен еншілес компонентке дерек жіберуге және оның көрінісін өзгертуге мүмкіндік береді. Мысалы, `Form` `Button` компонентіне `color` пропсын жібере алады.
* [**Күй** компоненттін жадысы сияқты.](/learn/state-a-components-memory) Ол компонентке деректерді сақтауға, бақылауға және оны өзгертуге мүмкіндік береді. Мысалы, `Button` `isHovered` күйі болуы мүмкін.

Пропс мен күй әртүрлі, бірақ олар бірге жұмыс істейді. Негізгі компонент ақпаратты көбінесе күйде сақтайды (оны өзгерте алады) және оны қосалқы компонент бөліктерге *жібереді*. Бірінші үйренгенде айырмашылықтары әлі де бұлыңғыр болуы мүмкін. Біраз тәжірибемен айырмашылық айқынырақ болады!

</DeepDive>

## 4-қадам: Сіздің күйініз қай жерде болуы керек екенін анықтаңыз {/*step-4-identify-where-your-state-should-live*/}

Қосымшаның күй деректерін анықтағаннан кейін, күйді өзгертуге қандай компонент жауапты немесе оған *иелік* ететінін анықтау керек. Есіңізде болсын: React бір жақты деректер ағынын пайдаланады, деректерді иерархия бойынша негізгі компоненттен еншілес компоненқа жібереді. Қай компонент қандай күйге ие болуы керектігі бірден анық болмауы мүмкін. Егер сіз бұл тұжырымдамамен таныс болсаңыз, бұл қиын болуы мүмкін, бірақ оны мына қадамдарды орындау арқылы анықтауға болады!

Әрбір cіздің қосымшаныздың күйі үшін: 

1. Осы күйге негізделген көрсететін *барлық* компоненттерді анықтаңыз.
2. Олардың ең жақын ортақ негізгі компонент бөлігін табыңыз - иерархиядағы барлығынан жоғары компонент.
3. Күйініз қай жерде болуы керектігін анықтаңыз::
    1. Көбінесе күйді олардың жалпы компонентіне қоюға болады.
    2. Сондай-ақ, күйді компоненттердің кез келгеніне олардың ортақ негізгі компонентінің үстіне қоюға болады.
    3. Егер сәйкес компонентті таба алмасаңыз, күйді сақтау үшін ғана жаңа компонент жасаңыз және оны жалпы негізгі компоненттін үстінгі иерархиясына орналастырыныз.

Алдыңғы қадамда демо қосымшада сіз екі күй бөлігін таптыңыз: іздеу енгізу мәтіні және чекбокс мәні. Бұл мысалда олар әрқашан бірге пайда болады, сондықтан оларды бір жерге қою мағынасы бар.

Енді олар үшін стратегиямызды қарастырайық:

1. **Identify components that use state:**
    * `ProductTable` needs to filter the product list based on that state (search text and checkbox value). 
    * `SearchBar` needs to display that state (search text and checkbox value).
2. **Find their common parent:** The first parent component both components share is `FilterableProductTable`.
3. **Decide where the state lives**: We'll keep the filter text and checked state values in `FilterableProductTable`.

Компонент күйді [`useState()` Hook](/reference/react/useState) арқылы қосамыз. Хуктар - бұл React-ке қосылуға мүмкіндік беретін арнайы "ілмек" функциялар. `FilterableProductTable` жоғарғы жағына екі күй айнымалы мәнін қосыңыз және олардың бастапқы күйін көрсетіңіз:

```js
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);  
```

`ProductTable` және `SearchBar` компоненттеріне `filterText` және `inStockOnly` пропстарын жіберініз:

```js
<div>
  <SearchBar 
    filterText={filterText} 
    inStockOnly={inStockOnly} />
  <ProductTable 
    products={products}
    filterText={filterText}
    inStockOnly={inStockOnly} />
</div>
```
Қосымшаныз қалай әрекет ететінін көре бастай аласыз. Төмендегі құмжәшіг кодындағы `filterText` бастапқы мәнін `useState('')` мәнінен `useState('fruit')` мәніне өзгертіңіз. Іздеу жүйесінің мәтінін де, кестенің де өзгергенін көресіз:

<Sandpack>

```jsx src/App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} />
      <ProductTable 
        products={products}
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 5px;
}
td {
  padding: 2px;
}
```

</Sandpack>

Форманы өңдеу әлі жұмыс істемейтінін ескеріңіз. Жоғарыдағы құмжәшігте консоль қатесі көрсетілген:

<ConsoleBlock level="error">

You provided a \`value\` prop to a form field without an \`onChange\` handler. This will render a read-only field.

</ConsoleBlock>

Жоғарыдағы құмжәшігте `ProductTable` және `SearchBar`, енгізуді және чекбокс көрсету үшін "filterText" және "inStockOnly" пропсын оқиды. Мысалы, `SearchBar` енгізу мәнін қалай толтырады:

```js {1,6}
function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
```
Дегенмен, теру сияқты пайдаланушы әрекеттеріне жауап беретін кодты әлі қосқан жоқсыз. Бұл сіздің соңғы қадамыңыз болады.


## 5-қадам: Кері деректер ағынын қосыңыз {/*step-5-add-inverse-data-flow*/}

Қазіргі уақытта компонентініз иерархияға төменге бағдарланған пропстармен мен күй негізінде рендірленеді. Дегенмен, пайдаланушы енгізуі негізінде күйдің өзгеруі үшін кері бағытта деректер ағынын қамтамасыз ету керек: иерархияның ең төменгі форма компоненттер `FilterableProductTable`-ге күйін жіберу керек.

React-те деректер ағыны бір бағытты. Осыған байланысты деректерді екі жақты байланыстыруға қарағанда сәл көбірек код қажет. Іздеу өрісіне мәтін енгізсеніз немесе чекбоксты бассаныз, React елемейтінін көресіз. Осылай болуы қажет. `<input value={filterText} />` қойған кезде, сіз инпутті `мән` пропасын әрқашан `FilterableProductTable` ішінен жіберілген `filterText` күйіне тең етіп орнаттыңыз. `filterText` күйі орнатылмағандықтан, инпут ешқашан өзгермейді.

Іздеу формасы өзгерген кезде енгізу күйінің өзгеруін қалаймыз. Күй `FilterableProductTable` иелігінде, сондықтан ол тек `setFilterText` және `setInStockOnly` шақыра алады. `SearchBar` `FilterableProductTable` күйін жаңарту үшін осы функцияларды `SearchBar` ішіне жіберу керек:

```js {2,3,10,11}
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />
```
`SearchBar` сіз `onChange` оқиға өңдегіштерін қосасыз және олардан негізгі күйді орнатасыз:

```js {4,5,13,19}
function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input
        type="text"
        value={filterText}
        placeholder="Search..."
        onChange={(e) => onFilterTextChange(e.target.value)}
      />
      <label>
        <input
          type="checkbox"
          checked={inStockOnly}
          onChange={(e) => onInStockOnlyChange(e.target.checked)}
```

Енді қосымша толығымен жұмыс істейді!

<Sandpack>

```jsx src/App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} 
        onFilterTextChange={setFilterText} 
        onInStockOnlyChange={setInStockOnly} />
      <ProductTable 
        products={products} 
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} placeholder="Search..." 
        onChange={(e) => onFilterTextChange(e.target.value)} />
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} 
          onChange={(e) => onInStockOnlyChange(e.target.checked)} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding: 4px;
}
td {
  padding: 2px;
}
```

</Sandpack>

Оқиғаларды өңдеу және күйді жаңарту туралы барлық ақпаратты [Интерактивтілікті қосу](/learn/adding-interactivity) бөлімінде біле аласыз.

## Ары қарай уйрену {/*where-to-go-from-here*/}

Бұл React көмегімен компонент пен қосымшаларды құру туралы қысқаша кіріспе болды. Сіз дәл қазір React арқылы жоба [бастай аласыз](/learn/installation) немесе осы оқулықта пайдаланылған [барлық синтаксисті тереңірек үйренуге](/learn/describing-the-ui) болады.
