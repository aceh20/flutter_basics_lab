# ANSWERS.md — Lab: Flutter Architecture, Widgets and Basic UI

**Name:** Aceh Aguanza
**Section:** BSIT3A-ILGX3
**Student ID:** 241-00023
**Course:** IT 120 — Integrative Programming and Technologies 2 (Weeks 10–11)

---

## 1. GitHub repository link

> I-fill paghuman nimo mag-push (Step 3 sa manual):

```
https://github.com/YOUR_USERNAME/flutter_basics_lab
```

---

## 2. Last three `build() called` lines from Activity 2

> Kuhaa gikan sa VS Code Debug Console (Ctrl+Shift+Y) samtang nagdagan ang Activity 2.
> I-tap ang + pipila ka beses una, kay magamit nimo kining format:

```
build() called: 4 glasses
build() called: 5 glasses
build() called: 6 glasses
```

---

## 3. Observations from the experiments

### Activity 2 — `_glasses++` outside `setState()`

Ang nahitabo: mitubo ang sulod nga `_glasses` (kung i-print nimo kini), **pero dili mag-usab ang
screen** — dili ma-update ang "0 / 8 glasses" nga teksto ug ang progress bar. Wa magamit ang `+`
button bisan og mikuptop ka.
**Ngano:** ang `setState()` mao ang nagasulti sa Flutter nga *"nausab ang akong data, palihug
pangayoa pag-usab ang `build()`"*. Kung wala kana, ang data naa na sa memory apan ang nawong sa
screen dili pa na-reload, hangtod naa laing magpahigayon og `setState()` (contoh: i-tap ang Reset
nga mogamit og `setState`, unya mobalik ang hustong numero sa screen). → Gibalik na sa code.

### Activity 3 — removing `Expanded` from one `StatBox`

Ang nahitabo: ang StatBox nga wala na'y `Expanded` **gihimo ra sa iyang kaugalingong kuwadradong
katas-on** (dili na bahin sa ika-tulo/tika-apat sa lapad) — dili na managsama ang upat ka boxes,
ug kung gamay ang bintana mahimo na kining **yellow/black stripes (overflow)**.
**Ngano:** ang `Row` naghatag og libreng lapad sa iyang mga anak; kung walay `Expanded`, ang
`Container` mohimo lang sa iyang klameng gikinahanglan (intrinsic width) ug dili kini moapil sa
pagbahinbahin sa available space. Ang `Expanded` mao ang nagapaambit og equal nga walahag sa
tanan. → Gibalik na.

### Activity 5 — button corner radius 8 → 20

Ang nahitabo: ang **ElevatedButton** (ug bisan asang ElevatedButton sa app) hingpit nga mas
**rounded/curved** ang mga kilay — gikan sa gamayng piso (8) ngadto sa halos bilog (20), apan
parehas gihapon ang padding. Kini nagapakita nga usa ra ka butang ang gi-usab sa `buildTheme()`
pero **tanang ElevatedButton sa tibuok app** nagbag-o, kay gikan kini sa `ThemeData`.

---

## 4. Review questions

### 1. Difference between StatelessWidget and StatefulWidget, with one example each

Ang **StatelessWidget** walay mabag-o nga data — ang `build()` niya magama lang kung magbag-o ang
iyang mga input (parent), ug ang na-draw mao gihapon hangtod usab-on kana. Example gikan sa lab:
`ProfileCard` (Activity 1) — ang ngalan, programa ug email dili gyud mobalik.
Ang **StatefulWidget** naa kini'y State object nga nagakahupot og mabag-o nga data, ug gamit ang
`setState()` mapugngan nimo ang Flutter nga pag-usabon ang screen. Example: `WaterTrackerPage`
(Activity 2) — ang `_glasses` mobuhi ug mobakus samtang gigamit ang app.

### 2. Why is a StatefulWidget written as two classes? What does each do?

Kay maglain ang **tinuod nga butang (widget)** og **nagbabag-o nga kahimtang (state)**.
- Ang *unang klase* (`WaterTrackerPage`) mao ang widget/configuration — kini immutable; ang buhat
  niya usa ra: `createState()` aron pagsibog sa iyang State.
- Ang *ikaladhang klase* (`_WaterTrackerPageState`) mao ang nagahupot sa `_glasses`, ang mga
  method (`_addGlass`, `_reset`) ug ang `build()`.
Gipalahi kini aron maayo nga mapreserbar ang estado sa pag-usab-usab sa tree, ug aron mangawat
ang data nga gikan sa config (widget) gamit ang `this.x` gikan sa State.

### 3. What happened when you changed `_glasses` outside `setState()`? Why?

Miusab ang sulod sa `_glasses` apan **dili ma-update ang screen** (dili mobar ang progreso, dili
mamalo ang numero). Ang `setState()` mao lang ang nagapasigabot og *marka* nga "nausab ang data →
pangayoog pag-usab og `build()`"; kung wala kana, ang Flutter wala mahibalo nga nausab na ang data,
ug dili mo-*rebuild* ang widget. Mabalik ra ang hustong panan-aw kung naa lay laing nag-setState
(sama sa Reset button).

### 4. Looking at the Debug Console in Activity 2, when is `build()` called?

Gitawag ang `build()` sa **kada higayon nga ang state ma-usab** human ang `setState()` — mao kana
ang matag tap sa `+`, `−` ug `Reset` (ug sa unang pag-abli sa page). Kada usa niini nagapakita og
usa ka "build() called: N glasses" linya sa Debug Console. Dili kini gitawag sa matag frame o sa
kada tap kung walay `setState()`.

### 5. Main axis and cross axis of a Row and of a Column

Ang **main axis** mao ang direksyon nga diin *naghatag* ang layout, ang **cross axis** mao ang
perpendicular niini.
- **Row:** main = **pahalapad (horizontal)**, cross = **patindog (vertical)**.
- **Column:** main = **patindog (vertical)**, cross = **pahalapad (horizontal)**.
Mao kini ang hinungdan nga `mainAxisAlignment` sa Row nagakatag sa daplin, samtang
`crossAxisAlignment` sa Row nagatino kung taas-on (top/center/bottom) — balik sa Column.

### 6. What happened when you removed `Expanded` from a StatBox? What does Expanded do?

Sa akong pagsulay, ang StatBox nga walay `Expanded` **dili na bahin sa pagbahin og kaparehas nga
lapad** — gihimo ra niya ang iyang gikinahanglan nga lapad, mao nga dili na managsama ang mga
kutob, ug mahimo nang **overflow (yellow at black stripes)** kung gamay ang bintana. Ang `Expanded`
mao ang nagapahulam og espasyo gikan sa `Row` (o `Column`) ug **napapbahinbahin equally** ang nahabilin
nga lapad sa iyang mga ginikanan — mao kini ang paagi nga pag-a-adjust sa width sa screen dili
magbag-o sa hitsura sa maayong paagi.

### 7. Why use `GridView.builder` instead of a Column with many children?

Kay ang **`GridView.builder` naggamit og lazy building** — ang `itemBuilder` tawgon *para lang sa
mga card nga tan-awon sa screen*, busa dili mabuhat ang tibuok listahan kada higayon (mas paspas
alang sa dugay nga listahan), ug kini **nascroll** sa mga setting sa `crossAxisCount` aron hingpit
nga mabahin sa mga kolum. Ang `Column` dili man mag-scroll, nagabuhat *tanang* children, ug kung
daghan kau mahimo kining **RenderFlex overflow** kay dili kini mohaom sa taas sa screen.

### 8. How do Stack and Positioned create the Best seller badge?

Ang **`Stack`** nagadraw sa iyang mga child *isnay-patong* (ang unang child sa ubos), ug gipili
kung asa matapos gamit ang **`Positioned`**. Ang *Center/Column* sa sulod sa Card mao ang nilalaman
sa kard (icon, ngalan, presyo), samtang ang badge usa ka pula/orangeng `Container` nga
`Positioned(top: 8, left: 8)` — gipintal kini **8 pixels gikan sa ibabaw ug 8 pixels gikan sa
wala**, mao nga naandam kini sa sulod sa Stack sa ibabaw sa nilalaman. Gigamit pud ang
**collection-if** (`if (item.bestSeller)`) aron idugang lang ang badge sa mga best seller.

### 9. ThemeData vs style on one widget

Ang **`ThemeData`** nagahimo og pamaagi sa **tibuok app gikan sa usa ka lugar** — pananglitan,
sa Activity 5 ang `buildTheme()` mao ang naghimo og `appBarTheme(centerTitle: true)` ug
`elevatedButtonTheme`, busa **tanang** AppBar nagtakna sa tunga ug **tanang** ElevatedButton
adunay 20-pixel nga rounded corners.
Ang **style sa usa ka widget** mao ang pag-usab sa *usa lang ka butang* — pananglitan, ang
`TextStyle(fontSize: 24, fontWeight: FontWeight.bold)` sa ngalan sa ProfileCard (Activity 1) o ang
`BoxDecoration(color: colors.primary, borderRadius: ...)` sa header Container sa Activity 3 —
kini dili makaapekto sa ubang widget. Sa Activity 5: ang `CircleAvatar(backgroundColor:
colors.primary)` sa ListTile mao ang per-widget styling.

### 10. Which widget holds the dark-mode state, and how does the change reach MaterialApp?

Ang estado (`_isDark`) gihupot sa **`_ThemeDemoAppState`** — ang State sa *pinaka-itaas nga*
StatefulWidget (`ThemeDemoApp`). Sa dihang gibira ang switch, ang `SettingsPage` (stateless) motawag
og `onDarkChanged(newValue)` → moabot kini ngadto sa `_setDark()` sa parent → giusab ang `_isDark`
sa `setState()` → na-rebuild ang `build()` sa `ThemeDemoApp` → karon ang `MaterialApp` nagdawat og
`themeMode: ThemeMode.dark`, busa gamiton na kini ang `darkTheme` sa lugar nga `theme`.
Kining paagiha gitawag nga **lifting state up** — ang `SettingsPage` nagpakita ug nagtawag lamang,
ang *nagmamantalya* sa estado mao ang parent.

---

> **Paatubangon (i-review pag-usab nimo niini sa imong kaugalingong pulong — mao kini ang giingon
> sa manual nga "in your own words"):** ang mga tubag sa ibabaw gidraft aron mabasa nimo, pero
> i-paraphrase nimo aron mohaom sa imong estilo. Ang §2 ug §3 kinahanglang kuhaon nimo sa tinuod
> nga pagdagan sa app (Debug Console + imong kaugalingong obserbasyon).
