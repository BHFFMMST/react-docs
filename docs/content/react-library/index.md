# Uvod u React.js biblioteku

Dobrodošli u kurikulum za React.js — biblioteku za izgradnju modernih korisničkih interfejsa. Ovaj dokument predstavlja vodič kroz prve faze učenja React-a: od postavljanja okruženja do upravljanja formama. Cilj je omogućiti temeljno razumijevanje koncepata na kojima se zasniva React aplikacija.

---

## Uvod u React

### Opis

React je deklarativna, efikasna i fleksibilna JavaScript biblioteka za izgradnju korisničkih interfejsa. Razvijen od strane Meta (bivši Facebook), React omogućava kreiranje složenih interfejsa pomoću malih, izolovanih dijelova koda zvanih *komponente*. U ovoj sekciji, upoznat ćemo se sa osnovama biblioteke, njezinim prednostima i načinom pokretanja prve aplikacije.

### Sadržaj

#### ▸ Šta je React?

React je open-source biblioteka fokusirana na izgradnju **komponentnog korisničkog interfejsa**. React ne pokriva cijeli "framework" ekosistem (kao Angular), već se prvenstveno bavi prikazivanjem podataka korisniku.

#### ▸ Zašto koristiti React?

- ✔️ Jednostavan model programiranja baziran na komponentama
- ✔️ Visoke performanse zahvaljujući Virtual DOM-u
- ✔️ Bogat ekosistem i aktivna zajednica
- ✔️ Podrška za server-side rendering i mobilne aplikacije (React Native)

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
