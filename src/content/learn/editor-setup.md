---
title: Редакторды конфигурациялау
---

<Intro>

Дұрыс конфигурацияланған редактор кодты оқуды анық және жазуды жылдамырақ етеді. Бұл кодтта қателескен кезде оларды табуға көмектеседі! Редакторды бірінші рет орнатып жатсаңыз немесе редакторыңызды реттеңіз келсе, бізде бірнеше ұсыныстар бар.

</Intro>

<YouWillLearn>

* Ең танымал редакторлар қандай
* Кодты автоматты түрде форматтау жолы

</YouWillLearn>

## Сіздің редакторыңыз {/*your-editor*/}

[VS Code](https://code.visualstudio.com/) бүгінгі таңда қолданылатын ең танымал редакторлардың бірі. Плагиндер жүйесінде кең таңдау бар және GitHub сияқты танымал қызметтермен жақсы біріктірілген. Төменде тізімделген мүмкіндіктердің көпшілігін VS Code-на плагиндер ретінде қосуға болады, бұл оны жоғары конфигурациялауға мүмкіндік береді!

React қауымдастығында қолданылатын басқа танымал мәтіндік редакторлар:

* [WebStorm](https://www.jetbrains.com/webstorm/) JavaScript үшін арнайы әзірленген орта.
* [Sublime Text](https://www.sublimetext.com/) JSX және TypeScript қолдауы бар, [синтаксистік ерекшелеу](https://stackoverflow.com/a/70960574/458193) және қораптан автотолтыру бар.
* [Vim](https://www.vim.org/) кез келген мәтін түрін жасау мен өзгертуді өте тиімді ету үшін жасалған жоғары конфигурацияланатын мәтіндік редактор. Ол UNIX жүйелерінің көпшілігінде және Mac OS жүйесінде «vi» командасымен шақырылады.

## Ұсынылатын мәтіндік редактор мүмкіндіктері {/*recommended-text-editor-features*/}

Кейбір редакторлар осы мүмкіндіктермен бірге келеді, бірақ басқалары кеңейтімді қосуды қажет етуі мүмкін. Сіз таңдаған редактордың қандай мүмкіндіктері бар екенін тексеріңіз!

### Линтинг {/*linting*/}

Код линтерлері сіз жазған кезде кодыңыздағы ақауларды тауып, оларды ертерек түзетуге көмектеседі. [ESLint](https://eslint.org/) — JavaScript үшін танымал опенсорс жоба.

* [React-қа ұсынылған ESLint конфигурациясын орнатыңыз](https://www.npmjs.com/package/eslint-config-react-app) ([Node орнатылғанына](https://nodejs.org/en/download/current/) көз жеткізіңіз!)
* [ESLint бағдарламасын VSCode редакторына орнатыныз](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

**Жобаңызға [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) ережелерін қосқаныңызға көз жеткізіңіз.** Өте маңызды және қиын қателерді ерте ұстайды. Біз ұсынылған [`eslint-config-react-app`](https://www.npmjs.com/package/eslint-config-react-app) пресет осылардын барлығын қамтиды.

### Форматтау {/*formatting*/}

Кодыңызды басқа адамдармен бөліскен кезде ең соңғы уайымдайтын нәрсе ол [табтар немесе бос орындар](https://www.google.com/search?q=tabs+vs+spaces)! Қуанышқа орай, [Prettier](https://prettier.io/) кодты алдын ала орнатылған ережелерге сәйкес форматтайды. Prettier-ді іске қосыңыз, сонда барлық қойған табтар, бос орындар, тырнақша түрі және т.б. конфигурацияға сәйкес келетіндей етіп өзгертіледі. Prettier файлды сақтаған кезде форматтауды іске қосылады, бұл сіздің жұмысынызды жеңілдетеді.
=========
The last thing you want to do when sharing your code with another contributor is get into a discussion about [tabs vs spaces](https://www.google.com/search?q=tabs+vs+spaces)! Fortunately, [Prettier](https://prettier.io/) will clean up your code by reformatting it to conform to preset, configurable rules. Run Prettier, and all your tabs will be converted to spaces—and your indentation, quotes, etc will also all be changed to conform to the configuration. In the ideal setup, Prettier will run when you save your file, quickly making these edits for you.

Мына қадамдарды орындау арқылы [VSCode ішінде Prettier кеңейтімін](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) орнатуға болады:

1. VS code іске қосыңыз
2. Жылдам ашуды пайдаланыңыз (Ctrl/Cmd+P)
3. `ext install esbenp.prettier-vscode` командасын жазыныз
4. Enter пернесін басыңыз

#### Сақтау кезінде форматтау {/*formatting-on-save*/}

Ең дұрысы, кодты әр сақтау кезінде форматтау керек. VS Code-да бұл үшін параметрлер бар!

1. VS Code iшінде `CTRL/CMD + SHIFT + P` пернелер тіркесімін басыныз.
2. "settings" теріңіз
3. Enter пернесін басыңыз
4. Іздеу жолағына "format on save" деп теріңіз.
5. "format on save" опциясына белгі қойылғанына көз жеткізіңіз!

> Егер ESLint форматтау ережелері болса, олар Prettier бағдарламасымен қайшы келуі мүмкін.[`eslint-config-prettier`](https://github.com/prettier/eslint-config-prettier) арқылы ESLint алдын ала орнатылған барлық форматтау ережелерін өшіруді ұсынамыз. ESLint *тек* логикалық қателерді анықтау үшін пайдаланылады. Pull request код біріктірудің алдында файлдардың форматтауына көз жеткізгіңіз келсе, үздіксіз біріктіру (continuous integration) жүйеңізде [`prettier --check`](https://prettier.io/docs/en/cli.html#--check командасын пайдаланыңыз.
