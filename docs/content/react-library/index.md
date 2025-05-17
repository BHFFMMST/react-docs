# React.js: Izgradnja Modernih Korisničkih Interfejsa

Dobrodošli u sveobuhvatni vodič za React.js, JavaScript biblioteku koja je revolucionirala način na koji gradimo dinamičke i interaktivne korisničke interfejse. Ovaj kurikulum je pažljivo dizajniran da vas provede kroz ključne aspekte React-a, počevši od osnovnih koncepata i postavljanja razvojnog okruženja, pa sve do naprednijih tema poput upravljanja stanjem, komunikacije među komponentama i rada s formama. Naš cilj je da vam pružimo čvrste temelje i duboko razumijevanje principa na kojima počivaju moderne React aplikacije, osposobljavajući vas da samostalno kreirate sofisticirane web aplikacije.

Bilo da ste početnik u svijetu web razvoja ili iskusni programer koji želi proširiti svoje vještine, ovaj vodič će vam pomoći da savladate React i iskoristite njegov puni potencijal.

---

## Dobrodošli u Svijet React-a

### Šta je React?

React je deklarativna, efikasna i izuzetno fleksibilna JavaScript biblioteka otvorenog koda, stvorena i održavana od strane kompanije Meta (nekadašnji Facebook) zajedno sa zajednicom individualnih developera i kompanija. Primarna svrha React-a je olakšavanje izgradnje kompleksnih, interaktivnih korisničkih interfejsa (UI) za web aplikacije. Ono što React izdvaja je njegov **komponentni pristup** razvoju.

Zamislite korisnički interfejs kao skupinu Lego kockica. Svaka kockica (komponenta u React-u) je nezavisna, ima svoju specifičnu funkciju i izgled, i može se kombinovati sa drugim kockicama da bi se izgradila veća i složenija struktura (kompletna aplikacija). Ove komponente mogu biti jednostavne kao dugme ili input polje, ili složene kao čitava navigaciona traka ili korisnički profil.

React se fokusira na "V" u MVC (Model-View-Controller) arhitekturi, odnosno na **View** sloj – ono što korisnik vidi i sa čime interaguje. On ne nameće stroga pravila o tome kako strukturirati ostatak aplikacije (npr. upravljanje podacima ili rutiranje), što mu daje fleksibilnost da se integriše sa mnogim drugim bibliotekama i framework-ovima.

### Zašto koristiti React?

- ✔️ **Jednostavan model programiranja baziran na komponentama:** React-ov komponentni model omogućava lako razumijevanje i održavanje koda. Svaka komponenta je izolovana i može se razvijati, testirati i koristiti nezavisno.
- ✔️ **Visoke performanse zahvaljujući Virtual DOM-u:** React koristi Virtual DOM - laganu kopiju stvarnog DOM-a. Kada dođe do promjene, React prvo ažurira Virtual DOM, a zatim efikasno sinhronizuje samo one delove stvarnog DOM-a koji su se promenili. Ovo značajno poboljšava performanse, posebno u složenim i dinamičnim aplikacijama.
- ✔️ **Bogati ekosistem i aktivna zajednica:** Kao jedna od najpopularnijih JavaScript biblioteka, React ima ogroman ekosistem alata, biblioteka i resursa. Bez obzira na to da li vam je potrebna pomoć oko specifičnog problema ili želite da naučite najbolje prakse, velika je verovatnoća da već postoji rešenje ili vodič u React zajednici.
- ✔️ **Podrška za server-side rendering i mobilne aplikacije (React Native):** React se može koristiti ne samo za izradu web aplikacija, već i za razvoj mobilnih aplikacija putem React Native-a, kao i za server-side rendering, što dodatno povećava njegovu svestranost i primenu.

#### ▸ SPA: Single Page Applications

React aplikacije se obično razvijaju kao **SPA**: stranica se učitava samo jednom, a svi ostali podaci se učitavaju dinamički putem JavaScript-a, bez reloadovanja cijele stranice.

#### ▸ Postavljanje okruženja

1. Instalirati [Node.js](https://nodejs.org/)
2. Inicijalizacija projekta pomoću `npm`, `yarn`, `pnpm`
3. Kreiranje projekta:
   ```bash
   npm create vite@latest moja-react-aplikacija -- --template react
   cd moja-react-aplikacija
   npm install
   npm run dev
   ```

## Osnove React-a

React se temelji na nekoliko ključnih koncepata koji omogućavaju njegovu moć i fleksibilnost. Razumijevanje ovih osnova ključno je za efikasno korištenje React-a.

### JSX (JavaScript XML)

JSX je sintaksna ekstenzija za JavaScript koja omogućava pisanje HTML-olikog koda unutar JavaScript datoteka. Iako nije obavezan za korištenje React-a, JSX olakšava kreiranje i razumijevanje strukture korisničkog interfejsa.

**Primjer JSX-a:**

```javascript
const element = <h1>Zdravo, svijete!</h1>;
```

Ovaj kod izgleda kao HTML, ali je zapravo JavaScript. Babel kompajler prevodi JSX u `React.createElement()` pozive. Gornji primjer bi bio preveden u:

```javascript
const element = React.createElement('h1', null, 'Zdravo, svijete!');
```

**Ugrađivanje izraza u JSX:**

Možete ugraditi bilo koji JavaScript izraz unutar vitičastih zagrada `{}` u JSX-u.

```javascript
const ime = 'React Developer';
const element = <h1>Zdravo, {ime}!</h1>;
```

**Atributi u JSX-u:**

JSX koristi camelCase konvenciju za nazive atributa (npr. `className` umjesto `class`, `onClick` umjesto `onclick`).

```javascript
const element = <div className="pozdrav">Zdravo!</div>;
```

### Komponente

Komponente su osnovni gradivni blokovi React aplikacija. One su nezavisni, ponovno upotrebljivi dijelovi koda koji enkapsuliraju logiku i prikaz određenog dijela korisničkog interfejsa. Postoje dvije glavne vrste komponenata:

**Funkcionalne komponente:**

Jednostavne JavaScript funkcije koje primaju `props` (svojstva) kao argument i vraćaju React elemente koji opisuju šta treba biti prikazano na ekranu.

```javascript
function Pozdrav(props) {
  return <h1>Zdravo, {props.ime}!</h1>;
}

// Korištenje komponente
const element = <Pozdrav ime="Student" />;
```

**Klasne komponente (Legacy):**

ES6 klase koje nasljeđuju `React.Component` i imaju `render()` metodu koja vraća React elemente. Iako su funkcionalne komponente s Hooks API-jem postale dominantan način pisanja komponenata, važno je razumjeti i klasne komponente jer se mogu naći u starijim projektima.

```javascript
class PozdravKlasa extends React.Component {
  render() {
    return <h1>Zdravo, {this.props.ime}!</h1>;
  }
}

// Korištenje komponente
const element = <PozdravKlasa ime="Student" />;
```

### Props (Svojstva)

`Props` (skraćeno od properties) su način na koji komponente primaju podatke od svojih roditeljskih komponenata. Props su **read-only**, što znači da komponenta ne smije mijenjati props koje je primila.

```javascript
function KorisnikKartica(props) {
  return (
    <div className="korisnik-kartica">
      <h2>{props.korisnickoIme}</h2>
      <p>Email: {props.email}</p>
    </div>
  );
}

// Proslijeđivanje props-a
<KorisnikKartica korisnickoIme="AnaAnic" email="ana.anic@example.com" />
```

### State (Stanje)

`State` omogućava komponentama da kreiraju i upravljaju vlastitim podacima koji se mogu mijenjati tokom vremena. Kada se stanje komponente promijeni, React automatski ponovno renderira komponentu kako bi prikazao ažurirane podatke.

**Korištenje state-a u funkcionalnim komponentama (sa `useState` Hook-om):**

```javascript
import React, { useState } from 'react';

function Brojac() {
  // Deklaracija state varijable 'broj' i funkcije 'postaviBroj' za njezino ažuriranje
  const [broj, postaviBroj] = useState(0);

  return (
    <div>
      <p>Trenutni broj: {broj}</p>
      <button onClick={() => postaviBroj(broj + 1)}>Povećaj</button>
      <button onClick={() => postaviBroj(broj - 1)}>Smanji</button>
    </div>
  );
}
```

**Korištenje state-a u klasnim komponentama:**

```javascript
class BrojacKlasa extends React.Component {
  constructor(props) {
    super(props);
    this.state = { broj: 0 };
  }

  povecajBroj = () => {
    this.setState({ broj: this.state.broj + 1 });
  }

  smanjiBroj = () => {
    this.setState({ broj: this.state.broj - 1 });
  }

  render() {
    return (
      <div>
        <p>Trenutni broj: {this.state.broj}</p>
        <button onClick={this.povecajBroj}>Povećaj</button>
        <button onClick={this.smanjiBroj}>Smanji</button>
      </div>
    );
  }
}
```

### Lifecycle Metode (Klasne komponente)

Klasne komponente imaju niz ugrađenih metoda koje se pozivaju u različitim fazama životnog ciklusa komponente. Neke od najvažnijih su:

-   `constructor()`: Poziva se prije nego što se komponenta montira. Koristi se za inicijalizaciju state-a i vezivanje metoda.
-   `render()`: Jedina obavezna metoda. Vraća React elemente.
-   `componentDidMount()`: Poziva se odmah nakon što se komponenta montira (ubaci u DOM). Idealno mjesto za dohvaćanje podataka s API-ja.
-   `componentDidUpdate(prevProps, prevState)`: Poziva se odmah nakon što dođe do ažuriranja (promjena props-a ili state-a). Nije pozvana pri inicijalnom renderiranju.
-   `componentWillUnmount()`: Poziva se neposredno prije nego što se komponenta demontira i uništi. Koristi se za čišćenje resursa (npr. otkazivanje tajmera, uklanjanje event listenera).

U funkcionalnim komponentama, ekvivalenti lifecycle metoda postižu se pomoću `useEffect` Hook-a.

### Event Handling

React ima vlastiti sistem za obradu događaja koji je sličan HTML DOM događajima, ali s nekoliko sintaksnih razlika (npr. `onClick` umjesto `onclick`, događaji se pišu camelCase).

```javascript
function GumbZaKlik() {
  function handleClick() {
    alert('Gumb je kliknut!');
  }

  return (
    <button onClick={handleClick}>
      Klikni me
    </button>
  );
}
```

### Conditional Rendering

Omogućava prikazivanje različitih komponenata ili elemenata ovisno o određenim uvjetima. To se može postići korištenjem standardnih JavaScript uvjeta poput `if` naredbi, ternarnog operatora ili logičkog `&&` operatora.

**Korištenje `if` naredbe:**

```javascript
function PozdravKorisniku(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <h1>Dobrodošli natrag!</h1>;
  }
  return <h1>Molimo prijavite se.</h1>;
}
```

**Korištenje ternarnog operatora:**

```javascript
function PorukaStatusa(props) {
  const jeOnline = props.jeOnline;
  return (
    <p>Korisnik je {jeOnline ? 'online' : 'offline'}.</p>
  );
}
```

**Korištenje logičkog `&&` operatora (inline if):**

```javascript
function PrikaziObavijesti(props) {
  const neprocitanePoruke = props.neprocitanePoruke;
  return (
    <div>
      <h1>Zdravo!</h1>
      {neprocitanePoruke.length > 0 &&
        <h2>
          Imate {neprocitanePoruke.length} nepročitanih poruka.
        </h2>
      }
    </div>
  );
}
```

### Liste i ključevi

Za prikazivanje listi elemenata u React-u, obično se koristi JavaScript `map()` funkcija. Svaki element liste mora imati jedinstveni `key` prop. Ključevi pomažu React-u da identificira koji su se itemi promijenili, dodali ili uklonili, što je važno za efikasno ažuriranje DOM-a.

```javascript
function ListaStavki(props) {
  const brojevi = props.brojevi;
  const listaElemenata = brojevi.map((broj) =>
    <li key={broj.toString()}>
      {broj}
    </li>
  );
  return (
    <ul>{listaElemenata}</ul>
  );
}

const brojevi = [1, 2, 3, 4, 5];
// <ListaStavki brojevi={brojevi} />
```
Ključevi trebaju biti stabilni, predvidljivi i jedinstveni među sibling elementima. Korištenje indeksa kao ključeva se ne preporučuje ako se redoslijed itema može promijeniti.

## Komunikacija između komponenata i Kompozicija

Efikasna komunikacija i kompozicija komponenata su srž izgradnje složenih React aplikacija.

### Komunikacija Roditelj-Dijete (Parent-to-Child)

Najčešći način komunikacije. Roditeljska komponenta prosljeđuje podatke dječjoj komponenti putem `props`.

```javascript
// Roditeljska komponenta
function ProfilKorisnika() {
  const korisnik = { ime: 'Pero Perić', godine: 30 };
  return <DetaljiKorisnika korisnik={korisnik} />;
}

// Dječja komponenta
function DetaljiKorisnika(props) {
  return (
    <div>
      <p>Ime: {props.korisnik.ime}</p>
      <p>Godine: {props.korisnik.godine}</p>
    </div>
  );
}
```

### Komunikacija Dijete-Roditelj (Child-to-Parent)

Dječja komponenta može komunicirati s roditeljskom komponentom prosljeđivanjem callback funkcije kao prop. Kada se u dječjoj komponenti dogodi neki događaj, ona poziva tu callback funkciju, prosljeđujući podatke roditelju.

```javascript
// Roditeljska komponenta
function KontrolnaPloca() {
  const [poruka, postaviPoruku] = useState('');

  function obradiPodatkeIzDjeteta(podaci) {
    postaviPoruku(`Podaci iz djeteta: ${podaci}`);
  }

  return (
    <div>
      <p>{poruka}</p>
      <DjecjaKomponenta posaljiPodatkeRoditelju={obradiPodatkeIzDjeteta} />
    </div>
  );
}

// Dječja komponenta
function DjecjaKomponenta(props) {
  const [unos, postaviUnos] = useState('');

  function handleChange(event) {
    postaviUnos(event.target.value);
  }

  function handleSubmit() {
    props.posaljiPodatkeRoditelju(unos); // Poziv callback funkcije
  }

  return (
    <div>
      <input type="text" value={unos} onChange={handleChange} />
      <button onClick={handleSubmit}>Pošalji podatke roditelju</button>
    </div>
  );
}
```

### Komunikacija između Sibling Komponenata

Sibling komponente (komponente na istom nivou hijerarhije) ne mogu direktno komunicirati. Komunikacija se obično odvija podizanjem state-a (`lifting state up`) na najbližeg zajedničkog roditelja. Taj roditelj onda prosljeđuje podatke i callback funkcije sibling komponentama putem props-a.

```javascript
// Roditeljska komponenta (zajednički predak)
function App() {
  const [vrijednost, postaviVrijednost] = useState('');

  function handlePrviSiblingPromjenu(novaVrijednost) {
    postaviVrijednost(novaVrijednost);
  }

  function handleDrugiSiblingPromjenu(novaVrijednost) {
    postaviVrijednost(novaVrijednost);
  }

  return (
    <div>
      <PrviSibling vrijednost={vrijednost} onPromjena={handlePrviSiblingPromjenu} />
      <DrugiSibling vrijednost={vrijednost} onPromjena={handleDrugiSiblingPromjenu} />
      <p>Trenutna zajednička vrijednost: {vrijednost}</p>
    </div>
  );
}

// Prva Sibling komponenta
function PrviSibling(props) {
  function handleChange(event) {
    props.onPromjena(event.target.value);
  }
  return <input type="text" value={props.vrijednost} onChange={handleChange} placeholder="Prvi Sibling Unos" />;
}

// Druga Sibling komponenta
function DrugiSibling(props) {
    function handleChange(event) {
    props.onPromjena(event.target.value);
  }
  return <input type="text" value={props.vrijednost} onChange={handleChange} placeholder="Drugi Sibling Unos" />;
}
```

Za složenije scenarije komunikacije, posebno u većim aplikacijama, koriste se alati za upravljanje stanjem poput **Context API-ja** ili biblioteka kao što su **Redux** ili **Zustand**.

### Kompozicija Komponenata

React potiče kompoziciju, gdje se komponente grade od drugih manjih, specijaliziranih komponenata. Ovo dovodi do modularnijeg, lakšeg za održavanje i ponovno upotreblivog koda.

**Containment (Zadržavanje):**

Neke komponente ne znaju unaprijed svoju djecu. Takve komponente mogu koristiti `props.children` da bi prikazale elemente koji su im proslijeđeni kao djeca.

```javascript
function Okvir(props) {
  return (
    <div className={'okvir okvir-' + props.boja}>
      {props.children} {/* Ovdje će se renderirati dječji elementi */}
    </div>
  );
}

function DobrodoslicaDialog() {
  return (
    <Okvir boja="plava">
      <h1 className="dialog-naslov">Dobrodošli</h1>
      <p className="dialog-poruka">
        Hvala što ste posjetili našu aplikaciju!
      </p>
    </Okvir>
  );
}
```

**Specijalizacija:**

Ponekad se komponente mogu smatrati "specijalnim slučajevima" općenitijih komponenata. To se može postići konfiguriranjem općenitije komponente putem props-a.

```javascript
function Dialog(props) {
  return (
    <div className="dialog">
      <h1 className="dialog-naslov">{props.naslov}</h1>
      <p className="dialog-poruka">{props.poruka}</p>
      {props.children}
    </div>
  );
}

function UpozorenjeDialog() {
  return (
    <Dialog
      naslov="Upozorenje!"
      poruka="Jeste li sigurni da želite nastaviti?"
    />
  );
}

function UspjehDialog(props) {
  return (
    <Dialog
      naslov="Uspjeh!"
      poruka={props.porukaUspjeha}
    />
  );
}
```
Ovdje `UpozorenjeDialog` i `UspjehDialog` specijaliziraju općenitiju `Dialog` komponentu.

## React Hooks (Osnove)

Hookovi su funkcije koje omogućavaju "kačenje" na React state i lifecycle značajke iz funkcionalnih komponenata. Uvedeni su u Reactu 16.8 i predstavljaju moderniji način pisanja React komponenata.

### Zašto Hookovi?

Prije Hookova, state i lifecycle metode bile su dostupne samo u klasnim komponentama. Hookovi rješavaju nekoliko problema:

-   **Ponavljanje logike state-a:** Hookovi omogućavaju izdvajanje logike state-a u ponovno upotrebljive funkcije (custom hooks).
-   **Složene komponente:** Klasne komponente mogu postati velike i teške za razumijevanje zbog miješanja logike u lifecycle metodama. Hookovi omogućavaju organiziranje logike po srodnim dijelovima.
-   **Klase mogu biti zbunjujuće:** `this` keyword, vezivanje metoda i općenito ES6 klase mogu biti prepreka za učenje Reacta.

### Osnovni Hookovi

#### ▸ `useState`

Omogućava dodavanje lokalnog state-a funkcionalnim komponentama.

-   **Sintaksa:** `const [state, setState] = useState(initialState);`
-   Prima inicijalno stanje kao argument.
-   Vraća niz sa dvije vrijednosti: trenutno stanje i funkciju za ažuriranje tog stanja.

```javascript
import React, { useState } from 'react';

function Prekidac() {
  const [jeUkljucen, postaviUkljucenost] = useState(false);

  return (
    <button onClick={() => postaviUkljucenost(!jeUkljucen)}>
      {jeUkljucen ? 'UKLJUČENO' : 'ISKLJUČENO'}
    </button>
  );
}
```

#### ▸ `useEffect`

Omogućava izvršavanje side effecta u funkcionalnim komponentama. Side effecti uključuju dohvaćanje podataka, postavljanje pretplata, ručno mijenjanje DOM-a, itd. `useEffect` je zamjena za `componentDidMount`, `componentDidUpdate`, i `componentWillUnmount` iz klasnih komponenata.

-   **Sintaksa:** `useEffect(() => { /* side effect logika */ return () => { /* cleanup logika */ }; }, [dependencies]);`
-   Prima funkciju koja sadrži side effect logiku.
-   Opcionalno, može vratiti cleanup funkciju koja se izvršava prije nego što se komponenta demontira ili prije sljedećeg izvršavanja effecta.
-   Opcionalno, prima niz zavisnosti (`dependencies`). Effect će se ponovno izvršiti samo ako se neka od zavisnosti promijeni.
    -   Ako je niz zavisnosti prazan (`[]`), effect se izvršava samo jednom nakon inicijalnog renderiranja (kao `componentDidMount`).
    -   Ako niz zavisnosti nije specificiran, effect se izvršava nakon svakog renderiranja.

**Primjer: Dohvaćanje podataka**

```javascript
import React, { useState, useEffect } from 'react';

function PodaciKorisnika({ korisnikId }) {
  const [korisnik, postaviKorisnika] = useState(null);
  const [loading, postaviLoading] = useState(true);

  useEffect(() => {
    postaviLoading(true);
    fetch(\`https://api.example.com/users/\${korisnikId}\`)
      .then(response => response.json())
      .then(data => {
        postaviKorisnika(data);
        postaviLoading(false);
      })
      .catch(error => {
        console.error("Greška pri dohvaćanju korisnika:", error);
        postaviLoading(false);
      });

    // Cleanup funkcija nije uvijek potrebna, ali je dobra praksa za npr. otkazivanje fetch-a
    return () => {
      // Ovdje bi se mogla otkazati fetch operacija ako je komponenta demontirana prije nego što završi
    };
  }, [korisnikId]); // Effect se ponovno izvršava ako se korisnikId promijeni

  if (loading) {
    return <p>Učitavanje...</p>;
  }

  if (!korisnik) {
    return <p>Korisnik nije pronađen.</p>;
  }

  return (
    <div>
      <h1>{korisnik.ime}</h1>
      <p>Email: {korisnik.email}</p>
    </div>
  );
}
```

**Primjer: Postavljanje naslova dokumenta**

```javascript
import React, { useState, useEffect } from 'react';

function BrojacNaslova() {
  const [broj, postaviBroj] = useState(0);

  useEffect(() => {
    // Ažurira naslov dokumenta nakon svakog renderiranja
    document.title = \`Kliknuli ste \${broj} puta\`;
  }, [broj]); // Ponovno izvrši samo ako se 'broj' promijeni

  return (
    <div>
      <p>Kliknuli ste {broj} puta</p>
      <button onClick={() => postaviBroj(broj + 1)}>
        Klikni me
      </button>
    </div>
  );
}
```

### Pravila Hookova

Postoje dva važna pravila koja se moraju poštovati prilikom korištenja Hookova:

1.  **Pozivati Hookove samo na najvišem nivou:** Ne pozivati Hookove unutar petlji, uvjeta ili ugniježdenih funkcija. Uvijek ih pozivati na vrhu vaše React funkcionalne komponente, prije bilo kakvog `return` statementa.
2.  **Pozivati Hookove samo iz React funkcija:** Ne pozivati Hookove iz običnih JavaScript funkcija. Pozivati ih samo iz React funkcionalnih komponenata ili iz custom Hookova.

Linter pluginovi (poput `eslint-plugin-react-hooks`) pomažu u automatskom provođenju ovih pravila.

### Custom Hookovi

Custom Hookovi su JavaScript funkcije čije ime počinje sa `use` i koje mogu pozivati druge Hookove. Omogućavaju izdvajanje logike komponenata u ponovno upotrebljive funkcije.

**Primjer: Custom Hook za praćenje širine prozora**

```javascript
import { useState, useEffect } from 'react';

function useSirinaProzora() {
  const [sirina, postaviSirinu] = useState(window.innerWidth);

  useEffect(() => {
    function handleResize() {
      postaviSirinu(window.innerWidth);
    }

    window.addEventListener('resize', handleResize);

    // Cleanup funkcija za uklanjanje event listenera
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []); // Prazan niz zavisnosti, izvršava se samo pri montiranju i demontiranju

  return sirina;
}

// Korištenje custom Hook-a u komponenti
function MojaKomponenta() {
  const sirinaProzora = useSirinaProzora();

  return <p>Širina prozora je: {sirinaProzora}px</p>;
}
```
Custom Hookovi su moćan alat za dijeljenje logike između komponenata bez potrebe za render props ili higher-order components (HOC).

## Stiliziranje u React-u

Postoji više načina za stiliziranje React komponenata. Izbor ovisi o veličini projekta, preferencijama tima i specifičnim potrebama.

### 1. Inline Styles

Stilovi se mogu primijeniti direktno na elemente koristeći `style` atribut. Vrijednost `style` atributa mora biti JavaScript objekt, gdje su ključevi camelCase verzije CSS svojstava, a vrijednosti su stringovi (ili brojevi za neka svojstva).

```javascript
function MojStiliziraniTekst() {
  const stilNaslova = {
    color: 'blue',
    fontSize: '24px', // '24px' umjesto samo 24
    paddingLeft: '10px',
    backgroundColor: '#f0f0f0'
  };

  return <h1 style={stilNaslova}>Ovo je stilizirani naslov</h1>;
}
```

**Prednosti:**
- Jednostavno za brze, dinamičke stilove.
- Enkapsulacija stila unutar komponente.

**Nedostaci:**
- Ograničene CSS mogućnosti (nema pseudo-klasa, media query-ja direktno).
- Može postati nepregledno za veći broj stilova.
- Performanse mogu biti lošije u nekim slučajevima u usporedbi s CSS datotekama.

### 2. Obične CSS datoteke

Najtradicionalniji pristup. Kreirate `.css` datoteku i importirate je u svoju komponentu (ili globalno u `index.js` ili `App.js`).

**`stilovi.css`:**
```css
.card {
  border: 1px solid #ccc;
  padding: 16px;
  margin: 8px;
  border-radius: 4px;
  box-shadow: 2px 2px 5px rgba(0,0,0,0.1);
}

.card-title {
  font-size: 1.5em;
  color: #333;
}
```

**`MojaKartica.js`:**
```javascript
import React from 'react';
import './stilovi.css'; // Importiranje CSS datoteke

function MojaKartica(props) {
  return (
    <div className="card">
      <h2 className="card-title">{props.naslov}</h2>
      <p>{props.sadrzaj}</p>
    </div>
  );
}

export default MojaKartica;
```

**Prednosti:**
- Poznat pristup.
- Puna podrška za sve CSS značajke.
- CSS može biti keširan od strane preglednika.

**Nedostaci:**
- Globalni scope CSS klasa može dovesti do konflikata imena (npr. ako dvije različite komponente koriste istu klasu `.button`).
- Teže je pratiti koji stilovi utječu na koju komponentu u velikim aplikacijama.

### 3. CSS Moduli

CSS Moduli rješavaju problem globalnog scope-a CSS klasa tako što lokaliziraju klase na nivou komponente. Kada importirate CSS datoteku kao modul (npr. `stilovi.module.css`), React (ili alat za build poput Webpacka ili Vitea) automatski generira jedinstvena imena klasa.

**`MojaTipka.module.css`:**
```css
.tipka { /* Originalno ime klase */
  background-color: dodgerblue;
  color: white;
  padding: 10px 20px;
  border: 2px solid palevioletred;
  border-radius: 5px;
  cursor: pointer;
}

.tipka:hover {
  background-color: royalblue;
}
```

**`MojaTipka.js`:**
```javascript
import React from 'react';
import stilovi from './MojaTipka.module.css'; // Importiranje kao modul

function MojaTipka(props) {
  // stilovi.tipka će imati generirano jedinstveno ime, npr. 'MojaTipka_tipka__aBcDe'
  return (
    <button className={stilovi.tipka}>
      {props.children}
    </button>
  );
}

export default MojaTipka;
```

**Prednosti:**
- Lokalni scope klasa, izbjegavaju se konflikti.
- Jasna veza između komponente i njenih stilova.
- Mogućnost korištenja istih imena klasa u različitim modulima bez problema.

**Nedostaci:**
- Zahtijeva specifično imenovanje datoteka (`.module.css`).
- Može biti malo teže dijeliti stilove između komponenata ako nije planirano.

### 4. CSS-in-JS Biblioteke

Ove biblioteke omogućavaju pisanje CSS-a direktno unutar JavaScript koda koristeći template literals ili objekte. Popularne biblioteke uključuju:

-   **Styled Components:** Koristi tagged template literals za definiranje stiliziranih komponenata.
-   **Emotion:** Sličan Styled Components, ali nudi i druge načine definiranja stilova (npr. `css` prop).
-   **JSS (JavaScript Style Sheets):** Koristi JavaScript objekte za definiranje stilova.

**Primjer sa Styled Components:**

Prvo, instalirajte biblioteku: `npm install styled-components` ili `yarn add styled-components`.

```javascript
import React from 'react';
import styled from 'styled-components';

// Kreiranje stilizirane komponente <Tipka>
const Tipka = styled.button\`
  background-color: palevioletred;
  color: white;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;

  &:hover {
    background-color: mediumvioletred;
  }

  // Stilovi se mogu bazirati na props-ima
  ${props => props.primary && \`
    background-color: white;
    color: palevioletred;
  \`}
\`;

function App() {
  return (
    <div>
      <Tipka>Obična Tipka</Tipka>
      <Tipka primary>Primarna Tipka</Tipka>
    </div>
  );
}

export default App;
```

**Prednosti:**
- Komponentno orijentirani stilovi.
- Dinamičko stiliziranje bazirano na props-ima je jednostavno.
- Automatsko prefiksiranje vendor prefiksa.
- Nema problema s konfliktima imena klasa.
- Mogućnost kreiranja tema.

**Nedostaci:**
- Dodatna biblioteka (povećava veličinu bundle-a).
- Može postojati blagi overhead u performansama (iako je obično zanemariv).
- Sintaksa može biti nova za neke developere.

### 5. Utility-First CSS Frameworks (npr. Tailwind CSS)

Tailwind CSS je popularan framework koji pruža skup nisko-razinskih utility klasa koje se mogu direktno primijeniti u HTML-u (ili JSX-u) za izgradnju korisničkog interfejsa. Umjesto pisanja prilagođenog CSS-a, kombinirate postojeće klase.

**Primjer sa Tailwind CSS:**

Prvo, potrebno je [instalirati i konfigurirati Tailwind CSS](https://tailwindcss.com/docs/installation) u vašem projektu.

```javascript
// Primjer komponente koja koristi Tailwind klase
function TailwindKartica() {
  return (
    <div className="max-w-sm mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl m-5">
      <div className="md:flex">
        <div className="md:flex-shrink-0">
          <img className="h-48 w-full object-cover md:w-48" src="/img/store.jpg" alt="Trgovina" />
        </div>
        <div className="p-8">
          <div className="uppercase tracking-wide text-sm text-indigo-500 font-semibold">Studija slučaja</div>
          <a href="#" className="block mt-1 text-lg leading-tight font-medium text-black hover:underline">Pronalaženje kupaca za vašu tvrtku</a>
          <p className="mt-2 text-gray-500">Početak s novim poslom može biti težak. Ovaj vodič će vam pomoći da pronađete svoje prve kupce.</p>
        </div>
      </div>
    </div>
  );
}
```

**Prednosti:**
- Brz razvoj UI-a.
- Konzistentan dizajn jer se koriste predefinirane klase.
- Nema potrebe za imenovanjem CSS klasa.
- CSS bundle je obično vrlo mali u produkciji jer se generiraju samo korištene klase (uz PurgeCSS/JIT).

**Nedostaci:**
- HTML/JSX može postati "zagušen" s mnogo klasa.
- Zahtijeva učenje Tailwind klasa.
- Manje fleksibilno za vrlo specifične ili jedinstvene dizajne bez dodatnog prilagođavanja.

### Koji pristup odabrati?

-   Za **male projekte** ili brze prototipove, **inline stilovi** ili **obične CSS datoteke** mogu biti dovoljni.
-   Za **srednje do velike projekte** gdje je važna modularnost i izbjegavanje konflikata, **CSS Moduli** ili **CSS-in-JS biblioteke** su dobar izbor.
-   Ako preferirate **utility-first pristup** i brzu izgradnju UI-a s konzistentnim dizajnom, **Tailwind CSS** je odlična opcija.

Često se u projektima koristi kombinacija pristupa. Na primjer, globalni stilovi i teme mogu biti definirani u običnim CSS datotekama, dok se specifični stilovi komponenata rješavaju pomoću CSS Modula ili CSS-in-JS.

## Rad sa Formama

Forme su ključni dio većine web aplikacija za prikupljanje korisničkog unosa. React pruža kontroliran način za rad s formama.

### Kontrolirane Komponente (Controlled Components)

U HTML-u, elementi forme poput `<input>`, `<textarea>`, i `<select>` obično održavaju vlastito stanje i ažuriraju ga na temelju korisničkog unosa. U Reactu, **kontrolirane komponente** su one gdje React stanje (obično u state-u komponente) postaje "jedini izvor istine" za vrijednost input polja.

To znači da:
1. Vrijednost input polja se postavlja iz React state-a.
2. Svaka promjena u input polju (npr. kucanje korisnika) pokreće funkciju koja ažurira React state.

```javascript
import React, { useState } from 'react';

function FormaImena() {
  const [ime, postaviIme] = useState(''); // 1. State za čuvanje vrijednosti inputa

  function handleChange(event) {
    postaviIme(event.target.value); // 2. Ažuriranje state-a pri svakoj promjeni
  }

  function handleSubmit(event) {
    alert('Poslano ime: ' + ime);
    event.preventDefault(); // Sprječava defaultno ponašanje forme (reload stranice)
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Ime:
        <input type="text" value={ime} onChange={handleChange} /> {/* Vrijednost inputa je vezana za state */}
      </label>
      <button type="submit">Pošalji</button>
    </form>
  );
}

export default FormaImena;
```

**Prednosti kontroliranih komponenata:**
- Vrijednost inputa je uvijek sinkronizirana s React state-om.
- Omogućava laku validaciju i manipulaciju unosa.
- Lakše je implementirati dinamičke forme.

### Različiti Tipovi Inputa

#### ▸ `textarea`

U HTML-u, `<textarea>` vrijednost se postavlja unutar taga: `<textarea>Neki tekst</textarea>`.
U Reactu, `<textarea>` koristi `value` atribut, slično kao `<input type="text">`.

```javascript
function FormaKomentara() {
  const [komentar, postaviKomentar] = useState('');

  function handleChange(event) {
    postaviKomentar(event.target.value);
  }

  return (
    <form>
      <label>
        Komentar:
        <textarea value={komentar} onChange={handleChange} />
      </label>
      <p>Vaš komentar: {komentar}</p>
    </form>
  );
}
```

#### ▸ `select` (Dropdown)

U HTML-u, odabrana vrijednost `<select>` taga se označava `selected` atributom na `<option>` elementu.
U Reactu, `value` atribut se postavlja na samom `select` tagu.

```javascript
function FormaOdabiraVoca() {
  const [odabranoVoce, postaviOdabranoVoce] = useState('kokos'); // Inicijalna vrijednost

  function handleChange(event) {
    postaviOdabranoVoce(event.target.value);
  }

  function handleSubmit(event) {
    alert('Vaše omiljeno voće je: ' + odabranoVoce);
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Odaberite omiljeno voće:
        <select value={odabranoVoce} onChange={handleChange}>
          <option value="grejpfrut">Grejpfrut</option>
          <option value="limeta">Limeta</option>
          <option value="kokos">Kokos</option>
          <option value="mango">Mango</option>
        </select>
      </label>
      <button type="submit">Pošalji</button>
    </form>
  );
}
```
Za `multiple` select, `value` atribut na `select` tagu može primiti niz vrijednosti: `<select multiple={true} value={['B', 'C']}>`.

### Rukovanje s Više Inputa

Kada imate više input polja, možete koristiti `name` atribut na svakom inputu i jednu `handleChange` funkciju za sve njih.

```javascript
import React, { useState } from 'react';

function Rezervacija() {
  const [unosi, postaviUnose] = useState({
    imeGosta: '',
    brojGostiju: 1,
    dolaziNaVeceru: true
  });

  function handleInputChange(event) {
    const target = event.target;
    const vrijednost = target.type === 'checkbox' ? target.checked : target.value;
    const ime = target.name;

    postaviUnose(stariUnosi => ({
      ...stariUnosi, // Kopiraj sve stare vrijednosti
      [ime]: vrijednost // Ažuriraj samo promijenjenu vrijednost
    }));
  }

  function handleSubmit(event) {
    alert(\`Ime: \${unosi.imeGosta}, Broj gostiju: \${unosi.brojGostiju}, Dolazi na večeru: \${unosi.dolaziNaVeceru}\`);
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Ime gosta:
        <input
          name="imeGosta"
          type="text"
          value={unosi.imeGosta}
          onChange={handleInputChange} />
      </label>
      <br />
      <label>
        Broj gostiju:
        <input
          name="brojGostiju"
          type="number"
          value={unosi.brojGostiju}
          onChange={handleInputChange} />
      </label>
      <br />
      <label>
        Dolazi na večeru:
        <input
          name="dolaziNaVeceru"
          type="checkbox"
          checked={unosi.dolaziNaVeceru}
          onChange={handleInputChange} />
      </label>
      <br />
      <button type="submit">Pošalji</button>
    </form>
  );
}

export default Rezervacija;
```
Korištenje computed property names `[ime]: vrijednost` omogućava dinamičko postavljanje ključa u objektu state-a.

### Validacija Unosa

Validacija se može obaviti unutar `handleChange` funkcije ili prilikom submita forme.

**Primjer: Jednostavna validacija prilikom submita**

```javascript
function FormaPrijave() {
  const [email, postaviEmail] = useState('');
  const [lozinka, postaviLozinku] = useState('');
  const [greske, postaviGreske] = useState({});

  function handleSubmit(event) {
    event.preventDefault();
    const noveGreske = {};

    if (!email) {
      noveGreske.email = 'Email je obavezan.';
    } else if (!/\\S+@\\S+\\.\\S+/.test(email)) {
      noveGreske.email = 'Email nije validan.';
    }

    if (!lozinka) {
      noveGreske.lozinka = 'Lozinka je obavezna.';
    } else if (lozinka.length < 6) {
      noveGreske.lozinka = 'Lozinka mora imati najmanje 6 znakova.';
    }

    postaviGreske(noveGreske);

    if (Object.keys(noveGreske).length === 0) {
      // Nema grešaka, pošalji podatke
      alert('Prijava uspješna!');
      // Ovdje bi išla logika slanja podataka na server
    }
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Email:</label>
        <input type="email" value={email} onChange={e => postaviEmail(e.target.value)} />
        {greske.email && <p style={{ color: 'red' }}>{greske.email}</p>}
      </div>
      <div>
        <label>Lozinka:</label>
        <input type="password" value={lozinka} onChange={e => postaviLozinku(e.target.value)} />
        {greske.lozinka && <p style={{ color: 'red' }}>{greske.lozinka}</p>}
      </div>
      <button type="submit">Prijavi se</button>
    </form>
  );
}
```

### Nekontrolirane Komponente (Uncontrolled Components)

Alternativa kontroliranim komponentama su **nekontrolirane komponente**. Kod njih, podaci forme se rukuju direktno od strane DOM-a, a ne React state-a. Da biste dobili vrijednosti iz DOM-a, koristite `ref`.

Iako su kontrolirane komponente preporučeni pristup u većini slučajeva, nekontrolirane komponente mogu biti korisne:
- Kada integrirate React s ne-React kodom.
- Za jednostavne forme gdje ne trebate trenutnu vrijednost inputa za validaciju ili dinamičke promjene.
- Za upravljanje fokusom, selekcijom teksta ili media playbackom.

```javascript
import React, { useRef } from 'react';

function NekontroliranaForma() {
  const inputRef = useRef(null); // Kreiranje ref-a

  function handleSubmit(event) {
    alert('Poslano ime: ' + inputRef.current.value); // Pristup vrijednosti preko ref.current.value
    event.preventDefault();
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Ime:
        <input type="text" ref={inputRef} /> {/* Povezivanje ref-a s input elementom */}
      </label>
      <button type="submit">Pošalji</button>
    </form>
  );
}
```
Za inpute tipa `file` (`<input type="file" />`), oni su uvijek nekontrolirani jer je njihova vrijednost read-only i može biti postavljena samo od strane korisnika.

### Biblioteke za Forme

Za složenije forme s naprednom validacijom, upravljanjem stanjem forme, i submit logikom, često se koriste specijalizirane biblioteke poput:

-   **Formik:** Popularna biblioteka koja olakšava rukovanje stanjem forme, validacijom (npr. s Yup-om) i submitom.
-   **React Hook Form:** Fokusirana na performanse i jednostavnost korištenja, oslanja se na Hookove i nekontrolirane komponente (iako podržava i kontrolirane).
-   **React Final Form:** Lagana i fleksibilna biblioteka bazirana na Final Form.

Ove biblioteke mogu značajno smanjiti količinu boilerplate koda potrebnog za kompleksne forme.

---

Ovaj pregled pokriva osnove rada s formama u Reactu. Kontrolirane komponente su temelj, ali važno je znati i za druge pristupe i alate koji mogu olakšati razvoj.