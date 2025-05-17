# React Data Manipulation: Upravljanje Podacima u React Aplikacijama

Manipulacija podacima je ključni dio razvoja modernih React aplikacija. Obuhvata načine dohvata, transformacije, pohrane, dijeljenja i optimizacije podataka, kako bi korisnički interfejs bio dinamičan, responzivan i pouzdan.

---

## 1. Uvod: Zašto je upravljanje podacima važno?

- **Predvidljivost:** Pravilno upravljanje podacima omogućava pouzdano ponašanje aplikacije.
- **Održavanje:** Lakše održavanje i nadogradnja koda.
- **Performanse:** Sprečava nepotrebna renderiranja i optimizira protok podataka.
- **Korisničko iskustvo:** Brže i tačnije prikazivanje informacija korisniku.

---

## 2. Izvori i tipovi podataka u Reactu

Podaci u React aplikaciji mogu dolaziti iz različitih izvora:

- **Lokalno stanje komponente** (`useState`)
- **Podaci iz parent komponente** (props)
- **Globalno stanje** (Context API, Redux, Zustand, Jotai...)
- **Eksterni izvori** (REST API, GraphQL, baze podataka)
- **Podaci iz URL-a** (React Router, query params)
- **Cache i Local Storage**

---

## 3. Upravljanje lokalnim stanjem (Local State)

Najosnovnija manipulacija podacima dešava se unutar komponente pomoću **useState** hooka.

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

---

## 4. Prijenos podataka (Props & Callback Functions)

Podaci se prosljeđuju iz parent komponente u child pomoću **props-a**. Za komunikaciju u suprotnom smjeru koristi se callback funkcija.

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

## 5. Lifting State Up (Podizanje state-a)

Kada dva ili više sibling komponenata dijele podatke, potrebno je podići state na najbližeg zajedničkog roditelja.

---

## 6. Globalno stanje i Context API

Za dijeljenje podataka kroz više komponenti koristi se **Context API** ili naprednije biblioteke (Redux, Zustand...).

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

---

## 7. Dohvaćanje podataka sa servera (Fetching Data)

Za dinamičke aplikacije podaci se često dohvaćaju iz API-ja pomoću **fetch** ili biblioteka kao što je **axios**. Najčešće se za ovo koristi **useEffect** hook.

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

---

## 8. Transformacija i filtriranje podataka

Često je potrebno transformirati, sortirati ili filtrirati podatke prije prikaza.

```javascript
const filtrirani = korisnici.filter(k => k.name.startsWith("A"));
const sortirani = korisnici.sort((a, b) => a.name.localeCompare(b.name));
```

---

## 9. Optimizacija performansi (useMemo, useCallback)

Kada se rade skupe operacije nad podacima, koristi se **useMemo** za memorisanje rezultata i **useCallback** za memorisanje funkcija.

```javascript
import { useMemo } from "react";

function Lista({ podaci }) {
  const sortirani = useMemo(
    () => podaci.sort((a, b) => a.ime.localeCompare(b.ime)),
    [podaci]
  );
  // ...
}
```

---

## 10. Rad sa formama i validacija

Forme su poseban slučaj manipulacije podacima. State inputa je pod React kontrolom, a validacija se može raditi ručno ili uz pomoć biblioteka (npr. Formik, React Hook Form).

```javascript
function Forma() {
  const [ime, setIme] = useState("");
  const [greska, setGreska] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    if (ime.length < 2) {
      setGreska("Ime mora imati bar 2 slova.");
    } else {
      setGreska("");
      alert("Podaci su validni!");
    }
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={ime} onChange={e => setIme(e.target.value)} />
      {greska && <span style={{ color: "red" }}>{greska}</span>}
      <button type="submit">Pošalji</button>
    </form>
  );
}
```

---

## 11. Keširanje i lokalna pohrana (LocalStorage, SessionStorage)

Za čuvanje podataka na klijentu koristi se Web Storage API.

```javascript
// Spremanje
localStorage.setItem("korisnik", JSON.stringify({ ime: "Ana" }));

// Dohvaćanje
const korisnik = JSON.parse(localStorage.getItem("korisnik"));
```

---

## 12. Najčešće greške i dobre prakse

- **Ne mutirati direktno state:** State se uvijek ažurira preko set funkcije.
- **Ne raditi skupe operacije u renderu:** Koristiti useMemo.
- **Koristiti jedinstvene ključeve kod listi:** Npr. ID iz baze.
- **Ne koristiti index kao key u listama** (osim ako lista nikada neće mijenjati redoslijed).

---

## 13. Napredne teme (kratak pregled)

- **Redux, Zustand, Jotai** — napredne biblioteke za globalno stanje.
- **React Query, SWR** — keširanje i sinhronizacija podataka sa serverom.
- **GraphQL** — napredno upravljanje i dohvat podataka.
- **Optimistic Updates** — prikazivanje promjena korisniku prije potvrde servera.

---

## Zaključak

Pravilno upravljanje podacima je temelj stabilnih, brzih i lako održivih React aplikacija. Počni s osnovama (`useState`, `props`, `useEffect`), a za veće aplikacije istraži naprednija rješenja za globalno stanje i optimizaciju performansi.

---

**Dodatni resursi:**
- [React dokumentacija](https://react.dev/learn)
- [React Patterns](https://reactpatterns.com/)
- [Awesome React](https://github.com/enaqx/awesome-react)
