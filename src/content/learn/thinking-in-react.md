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

* **Программалау**--қарапайым функцияны немесе объект жасау туралы шешім қабылдаған кездегі тәсілді қолданыңыз. Техниканың бірі [single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle), бір компонент бір тапсырманы орындауы тиіс. Егер функционал уақыт өте келе ұлғайса, оны кішірек ішкі құрамдастарға бөлу керек.
* **CSS**--ойлаңыз, неліктен класс селектірін жасайтындығыңызды. (Дегенмен компоненттер соншалықты кішірейтілмегенін есте сақтаңыз.)
* **Дизайн**--дизайн қабаттарын қалай ұйымдастыратыныңызды ойлаңыз.

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

```jsx App.js
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

1. **Күйлерді қолданатын компоненттерді анықтаңыз:**
    * `ProductTable` күйлерге негізделген өнімдер тізімін фильтрлеу (іздеу сұрауы және чекбокс ұяшығының мәні).
    * `SearchBar` сол күйді көрсету керек (іздеу мәтіні және чекбокс мәні).
1. **Олардың ортақ негізгі компонентін табыңыз:** The first parent component both components share is `FilterableProductTable`.
2. **Күй қайда тұратынын шешіңіз**: We'll keep the filter text and checked state values in `FilterableProductTable`.

So the state values will live in `FilterableProductTable`. 

Add state to the component with the [`useState()` Hook.](/reference/react/useState) Hooks are special functions that let you "hook into" React. Add two state variables at the top of `FilterableProductTable` and specify their initial state:

```js
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);  
```

Then, pass `filterText` and `inStockOnly` to `ProductTable` and `SearchBar` as props:

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

You can start seeing how your application will behave. Edit the `filterText` initial value from `useState('')` to `useState('fruit')` in the sandbox code below. You'll see both the search input text and the table update:

<Sandpack>

```jsx App.js
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

Notice that editing the form doesn't work yet. There is a console error in the sandbox above explaining why:

<ConsoleBlock level="error">

You provided a \`value\` prop to a form field without an \`onChange\` handler. This will render a read-only field.

</ConsoleBlock>

In the sandbox above, `ProductTable` and `SearchBar` read the `filterText` and `inStockOnly` props to render the table, the input, and the checkbox. For example, here is how `SearchBar` populates the input value:

```js {1,6}
function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
```

However, you haven't added any code to respond to the user actions like typing yet. This will be your final step.


## Step 5: Add inverse data flow {/*step-5-add-inverse-data-flow*/}

Currently your app renders correctly with props and state flowing down the hierarchy. But to change the state according to user input, you will need to support data flowing the other way: the form components deep in the hierarchy need to update the state in `FilterableProductTable`. 

React makes this data flow explicit, but it requires a little more typing than two-way data binding. If you try to type or check the box in the example above, you'll see that React ignores your input. This is intentional. By writing `<input value={filterText} />`, you've set the `value` prop of the `input` to always be equal to the `filterText` state passed in from `FilterableProductTable`. Since `filterText` state is never set, the input never changes.

You want to make it so whenever the user changes the form inputs, the state updates to reflect those changes. The state is owned by `FilterableProductTable`, so only it can call `setFilterText` and `setInStockOnly`. To let `SearchBar` update the `FilterableProductTable`'s state, you need to pass these functions down to `SearchBar`:

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

Inside the `SearchBar`, you will add the `onChange` event handlers and set the parent state from them:

```js {5}
<input 
  type="text" 
  value={filterText} 
  placeholder="Search..." 
  onChange={(e) => onFilterTextChange(e.target.value)} />
```

Now the application fully works!

<Sandpack>

```jsx App.js
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

You can learn all about handling events and updating state in the [Adding Interactivity](/learn/adding-interactivity) section.

## Where to go from here {/*where-to-go-from-here*/}

This was a very brief introduction to how to think about building components and applications with React. You can [start a React project](/learn/installation) right now or [dive deeper on all the syntax](/learn/describing-the-ui) used in this tutorial.
