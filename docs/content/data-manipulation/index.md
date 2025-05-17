# React Data Manipulation: Upravljanje Podacima u React Aplikacijama

---

**Sadržaj**

1. [Uvod: Zašto upravljanje podacima?](#1-uvod-zašto-upravljanje-podacima)
2. [Vrste i izvori podataka u Reactu](#2-vrste-i-izvori-podataka-u-reactu)
3. [Osnovni koncepti manipulacije podacima](#3-osnovni-koncepti-manipulacije-podacima)
4. [Korištenje lokalnog stanja (useState)](#4-korištenje-lokalnog-stanja-usestate)
5. [Props: prijenos podataka među komponentama](#5-props-prijenos-podataka-među-komponentama)
6. [Podizanje state-a ("Lifting State Up")](#6-podizanje-state-a-lifting-state-up)
7. [Globalno stanje i Context API](#7-globalno-stanje-i-context-api)
8. [Napredne biblioteke za upravljanje stanjem](#8-napredne-biblioteke-za-upravljanje-stanjem)
9. [Dohvaćanje podataka s API-ja i serverska komunikacija](#9-dohvaćanje-podataka-s-api-ja-i-serverska-komunikacija)
10. [Transformacija, filtriranje i prikaz podataka](#10-transformacija-filtriranje-i-prikaz-podataka)
11. [Rad sa listama i ključevima](#11-rad-sa-listama-i-kljucevima)
12. [Optimizacija performansi](#12-optimizacija-performansi)
13. [Forme: upravljanje unosom i validacija](#13-forme-upravljanje-unosom-i-validacija)
14. [Nekontrolirane komponente i rad s ref-ovima](#14-nekontrolirane-komponente-i-rad-s-ref-ovima)
15. [Keširanje i lokalna pohrana](#15-keširanje-i-lokalna-pohrana)
16. [Najčešće greške i dobre prakse](#16-najčešće-greške-i-dobre-prakse)
17. [Napredne teme i korisni alati](#17-napredne-teme-i-korisni-alati)
18. [Dodatni resursi](#19-dodatni-resursi)

---

## 1. Uvod: Zašto upravljanje podacima?

Upravljanje podacima je temelj svake ozbiljne React aplikacije. Bez jasnog plana kako ćete dohvatiti, transformirati, dijeliti i prikazivati podatke, aplikacija brzo postaje neodrživa, spora i puna bugova. Dobar sistem za data manipulation donosi:

- Predvidljivo ponašanje aplikacije (nema iznenadnih grešaka ili nelogičnosti)
- Lakše održavanje i skaliranje koda
- Bolje korisničko iskustvo (brži UI, manje bugova)
- Veću fleksibilnost za integraciju s drugim servisima i API-jima

Praktično, svaki put kada korisnik klikne dugme, popuni formu, ili kad aplikacija treba prikazati listu stavki — radi se neka vrsta manipulacije podacima.

---

## 2. Vrste i izvori podataka u Reactu

Podaci u React aplikacijama dolaze iz različitih izvora, a razumijevanje izvora je ključno za pravilan dizajn aplikacije.

**Najčešći izvori podataka:**

- **Lokalno stanje komponente** (`useState`, `useReducer`)
- **Props** (podaci koje komponenta prima od roditelja)
- **Globalno stanje** (Context API, Redux, Zustand, Recoil, Jotai, MobX)
- **Eksterni API ili baza podataka** (REST API, GraphQL, Firebase...)
- **URL parametri i ruter** (React Router, search params, hash, pathname)
- **Lokalna pohrana** (LocalStorage, SessionStorage, IndexedDB)
- **Cache sloj** (React Query, SWR, Apollo Client...)

---

## 3. Osnovni koncepti manipulacije podacima

**React Data Manipulation** se odnosi na sve tehnike i obrasce kojima kontroliramo kako se podaci kreću kroz aplikaciju. Važno je shvatiti razliku između:

- **Jednosmjernog toka podataka** (data flow) — podaci idu od roditelja ka djetetu preko props-a.
- **Dvosmjernog toka podataka** — obično postižemo preko callback funkcija ili state management alata.

Kada planirate aplikaciju, uvijek postavite ova pitanja:

1. Gdje nastaje podatak? (input, API, generisan kodom)
2. Ko sve treba taj podatak?
3. Ko smije da ga mijenja?
4. Kako će promjena podatka utjecati na UI?

---

## 4. Korištenje lokalnog stanja (useState)

Lokalni state je najosnovniji način za upravljanje podacima unutar jedne komponente.

```javascript
import { useState } from 'react';

function Brojac() {
  const [count, setCount] = useState(0);

  const povecaj = () => setCount(prev => prev + 1);
  const smanji = () => setCount(prev => prev - 1);
  const resetiraj = () => setCount(0);

  return (
    <div>
      <p>Trenutna vrijednost: {count}</p>
      <button onClick={povecaj}>+</button>
      <button onClick={smanji}>-</button>
      <button onClick={resetiraj}>Reset</button>
    </div>
  );
}
```

**Kada koristiti lokalni state?**

- Kada podatak treba samo toj komponenti.
- Kada podatak ne utiče na druge dijelove aplikacije.
- Za privremene UI efekte (modali, animacije, hover state...)

---

## 5. Props: prijenos podataka među komponentama

**Props** (properties) su osnovni način komunikacije od roditeljske ka djetetovoj komponenti. Props su read-only i ne mogu se mijenjati unutar djeteta.

```javascript
function Pozdrav({ ime }) {
  return <h2>Zdravo, {ime}!</h2>;
}

function App() {
  return <Pozdrav ime="Amar" />;
}
```

**Kako dijete šalje podatke roditelju?**  
Kroz callback funkciju proslijeđenu kao prop.

```javascript
function Parent() {
  const [poruka, setPoruka] = useState("");

  function primiPoruku(novaPoruka) {
    setPoruka(novaPoruka);
  }

  return (
    <>
      <Child posaljiRoditelju={primiPoruku} />
      <p>Poruka iz djeteta: {poruka}</p>
    </>
  );
}

function Child({ posaljiRoditelju }) {
  return <button onClick={() => posaljiRoditelju("Pozdrav iz djeteta!")}>Pošalji roditelju</button>;
}
```

---

## 6. Podizanje state-a ("Lifting State Up")

Kada dva ili više sibling komponenata treba da dijele podatke, najbolje rješenje je podići state na njihovog zajedničkog roditelja.

**Primjer:**

```javascript
function Kontrola() {
  const [vrijednost, setVrijednost] = useState("");

  return (
    <div>
      <InputA vrijednost={vrijednost} setVrijednost={setVrijednost} />
      <InputB vrijednost={vrijednost} setVrijednost={setVrijednost} />
      <p>Trenutna zajednička vrijednost: {vrijednost}</p>
    </div>
  );
}

function InputA({ vrijednost, setVrijednost }) {
  return <input value={vrijednost} onChange={e => setVrijednost(e.target.value)} placeholder="A" />;
}

function InputB({ vrijednost, setVrijednost }) {
  return <input value={vrijednost} onChange={e => setVrijednost(e.target.value)} placeholder="B" />;
}
```

---

## 7. Globalno stanje i Context API

Kada podaci trebaju da budu dostupni na više mjesta u aplikaciji (npr. user info, tema, jezik), koristi se Context API ili globalni state manageri.

```javascript
import React, { createContext, useContext, useState } from "react";

const UserContext = createContext();

function App() {
  const [user, setUser] = useState({ ime: "Ana" });

  return (
    <UserContext.Provider value={user}>
      <Profil />
    </UserContext.Provider>
  );
}

function Profil() {
  const user = useContext(UserContext);
  return <h2>Korisnik: {user.ime}</h2>;
}
```

**Napomena:**  
Nemojte koristiti Context za često mijenjane podatke ili velike objekte (može usporiti renderiranje).

---

## 8. Napredne biblioteke za upravljanje stanjem

Za kompleksne aplikacije, često koristimo naprednije alate:

- **Redux** — industrijski standard, predvidiv, ali ima više boilerplate koda.
- **Zustand** — jednostavan i lagan, koristi hooks.
- **Recoil, Jotai, MobX** — savremene alternative za različite potrebe.
- **React Query / TanStack Query** — za rad sa server state-om (fetch, cache, sync).

**Primjer Redux slice-a:**

```javascript
// features/user/userSlice.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = { ime: '', prijavljen: false };

const userSlice = createSlice({
  name: 'user',
  initialState,
  reducers: {
    prijavi: (state, action) => {
      state.ime = action.payload;
      state.prijavljen = true;
    },
    odjavi: (state) => {
      state.ime = '';
      state.prijavljen = false;
    }
  }
});

export const { prijavi, odjavi } = userSlice.actions;
export default userSlice.reducer;
```

---

## 9. Dohvaćanje podataka s API-ja i serverska komunikacija

Dohvaćanje podataka često se radi u `useEffect` hooku, ili pomoću biblioteka (React Query, SWR, Axios).

```javascript
import React, { useState, useEffect } from "react";

function ListaKorisnika() {
  const [korisnici, setKorisnici] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => {
        setKorisnici(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Učitavanje...</p>;
  return (
    <ul>
      {korisnici.map(k => (
        <li key={k.id}>{k.name}</li>
      ))}
    </ul>
  );
}
```

**Bitne napomene:**
- **Error handling:** Uvijek hvataj greške kod dohvata podataka.
- **Cleanup:** Ako koristiš async logiku u useEffect, vodi računa o otkazivanju fetch-a.

---

## 10. Transformacija, filtriranje i prikaz podataka

U praksi, podatke često treba transformirati prije prikaza: filtrirati, sortirati, grupisati, mapirati.

```javascript
const filtrirani = korisnici.filter(k => k.name.startsWith("A"));
const sortirani = korisnici.sort((a, b) => a.name.localeCompare(b.name));
const imena = korisnici.map(k => k.name.toUpperCase());
```

**Primjer prikaza filtrirane liste:**

```javascript
function PrikazFiltriranih({ korisnici }) {
  const filtrirani = korisnici.filter(k => k.name.length > 5);
  return (
    <ul>
      {filtrirani.map(k => <li key={k.id}>{k.name}</li>)}
    </ul>
  );
}
```

---

## 11. Rad sa listama i ključevima

Svaki element u listi mora imati jedinstveni `key` prop. Najbolje koristiti ID iz baze.

```javascript
const brojevi = [1, 2, 3, 4, 5];
<ul>
  {brojevi.map(broj => <li key={broj}>{broj}</li>)}
</ul>
```

**Zašto ne koristiti index kao key?**
Ako se redoslijed promijeni, React može pogrešno interpretirati koji je element koji, što vodi do bugova.

---

## 12. Optimizacija performansi

Za kompleksne aplikacije i velike podatke, koristi:

- **useMemo** — memorisanje izračuna
- **useCallback** — memorisanje funkcija
- **React.memo** — sprječava nepotrebno renderiranje child komponenti

```javascript
import { useMemo } from "react";

function Lista({ podaci }) {
  const sortirani = useMemo(
    () => podaci.slice().sort((a, b) => a.ime.localeCompare(b.ime)),
    [podaci]
  );
  // ...
}
```

**Primjer React.memo:**

```javascript
const Dugme = React.memo(function Dugme({ onClick, label }) {
  return <button onClick={onClick}>{label}</button>;
});
```

---

## 13. Forme: upravljanje unosom i validacija

### 13.1 Kontrolirane forme

React forme se najčešće rade kao kontrolirane komponente — vrijednost inputa se čuva u state-u.

```javascript
function FormaImena() {
  const [ime, setIme] = useState('');

  function handleChange(event) {
    setIme(event.target.value);
  }

  function handleSubmit(event) {
    event.preventDefault();
    alert('Uneseno ime: ' + ime);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={ime} onChange={handleChange} />
      <button type="submit">Pošalji</button>
    </form>
  );
}
```

### 13.2 Višestruki inputi i objekat u state-u

```javascript
function Rezervacija() {
  const [unosi, setUnosi] = useState({
    imeGosta: '',
    brojGostiju: 1,
    dolaziNaVeceru: true
  });

  function handleInputChange(event) {
    const { name, type, value, checked } = event.target;
    setUnosi(stari => ({
      ...stari,
      [name]: type === 'checkbox' ? checked : value
    }));
  }

  // ... ostatak forme kao prije
}
```

### 13.3 Validacija unosa

Validaciju možeš raditi ručno ili pomoću biblioteka (Formik, React Hook Form, Yup).

```javascript
function FormaPrijave() {
  const [email, setEmail] = useState('');
  const [lozinka, setLozinka] = useState('');
  const [greske, setGreske] = useState({});

  function handleSubmit(event) {
    event.preventDefault();
    const noveGreske = {};
    if (!email) {
      noveGreske.email = 'Email je obavezan.';
    } else if (!/\S+@\S+\.\S+/.test(email)) {
      noveGreske.email = 'Email nije validan.';
    }

    if (!lozinka || lozinka.length < 6) {
      noveGreske.lozinka = 'Lozinka mora imati najmanje 6 znakova.';
    }

    setGreske(noveGreske);

    if (Object.keys(noveGreske).length === 0) {
      alert('Prijava uspješna!');
    }
  }

  // ... ostatak komponente
}
```

---

## 14. Nekontrolirane komponente i rad s ref-ovima

Nekontrolirane komponente koriste se kada ne želiš da React upravlja vrijednošću inputa, nego direktno pristupaš DOM-u putem ref-a.

```javascript
import React, { useRef } from 'react';

function NekontrolisanaForma() {
  const inputRef = useRef(null);

  function handleSubmit(event) {
    event.preventDefault();
    alert('Vrijednost iz inputa: ' + inputRef.current.value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input ref={inputRef} />
      <button type="submit">Pošalji</button>
    </form>
  );
}
```

**Kada koristiti?**
- Integracija sa starijim bibliotekama
- File inputi (`<input type="file" />`)
- Fokusiranje i selektovanje teksta

---

## 15. Keširanje i lokalna pohrana

Za čuvanje podataka na klijent strani koristi se LocalStorage, SessionStorage, ili specijalizirane biblioteke.

```javascript
// Spremanje podataka
localStorage.setItem('tema', 'tamna');

// Dohvaćanje podataka
const tema = localStorage.getItem('tema');
```

**Napomena:**  
Podaci u LocalStorage su stringovi, pa koristi JSON.stringify i JSON.parse za objekte.

---

## 16. Najčešće greške i dobre prakse

- **Ne mijenjaj state direktno** — koristi set funkcije.
- **Ne koristi index kao key kod lista** — koristi jedinstveni ID.
- **Ne koristi Context API za podatke koji se često mijenjaju** — može usporiti aplikaciju.
- **Ne radi skupe operacije u render funkciji** — koristi useMemo.
- **Uvijek hvataj greške kod fetch-a** — korisnik mora znati šta se dešava.
- **Ne dupliciraj podatke u više mjesta** — vodi brigu o izvoru istine (single source of truth).
- **Rasporedi odgovornosti** — neka svaka komponenta ima jasnu svrhu.

---

## 17. Napredne teme i korisni alati

- **Redux Toolkit** — pojednostavljeno upravljanje Reduxom
- **React Query / TanStack Query** — automatsko keširanje, refetch, stale-while-revalidate
- **SWR** — jednostavno keširanje i revalidacija podataka
- **Apollo Client** — GraphQL client s cache-iranjem
- **Zustand, Jotai, Recoil** — moderne alternative Reduxu
- **Immer** — za imutabilno ažuriranje stanja bez puno koda
- **XState** — za modeliranje složenih state-ova kao finite state machine

---



## 19. Dodatni resursi

- [React dokumentacija](https://react.dev/learn)
- [React Patterns](https://reactpatterns.com/)
- [Awesome React](https://github.com/enaqx/awesome-react)
- [Redux Toolkit](https://redux-toolkit.js.org/)
- [React Query](https://tanstack.com/query/latest)
- [Formik](https://formik.org/)
- [React Hook Form](https://react-hook-form.com/)
- [GraphQL](https://graphql.org/)

---

**Napomena:** Ovu dokumentaciju slobodno koristi, prilagodi i proširi prema potrebama svog projekta ili tima. Praktični primjeri su tu da olakšaju razumijevanje, ali uvijek eksperimentiraj i istražuj službenu dokumentaciju za najnovije najbolje prakse i alate.

---
