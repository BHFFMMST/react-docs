# Moodflix 🎬

Dobrodošli u **Moodflix**, jednostavnu React aplikaciju koja preporučuje filmove na osnovu vašeg trenutnog raspoloženja.

Cilj ove aplikacije je demonstrirati rad sa osnovnim konceptima React-a, poput upravljanja stanjima (`useState`), efekata (`useEffect`), komunikacije između komponenti, kao i jednostavne logike za prikaz podataka.

Moodflix omogućava korisnicima da izaberu svoje trenutno **raspoloženje** (npr. sretan, tužan, opušten), nakon čega im aplikacija prikazuje odgovarajuće filmske preporuke. Aplikacija može koristiti statički set podataka ili biti proširena da koristi eksterni API (npr. TMDB API).

Ovaj projekat je kreiran kao edukativni primjer za radionicu i služi kao osnova za učenje rada sa React komponentama, stilizacijom i prikazom dinamičkog sadržaja.

## Tehnologije koje se koriste

Moodflix je izgrađen korištenjem modernog React ekosistema i alata za razvoj brzih i responsivnih web aplikacija. U nastavku su navedene ključne tehnologije korištene u ovom projektu:

### 🎯 Frontend

- **React** (`v18.3.1`) – JavaScript biblioteka za izgradnju korisničkih interfejsa.
- **React Router DOM** (`v6.26.2`) – Za upravljanje rutama i navigacijom unutar aplikacije.
- **Tailwind CSS** (`v3.4.13`) – Utility-first CSS framework za brzo i elegantno stilizovanje korisničkog interfejsa.
- **PropTypes** (`v15.8.1`) – Za tipizaciju props-a u komponentama.

### 🚀 Razvoj i build alati

- **Vite** (`v5.4.8`) – Ultra brzi build alat i dev server.
- **ESLint** (`v9.11.1`) – Alat za statičku analizu koda i osiguranje konzistentnog stila koda.
- **PostCSS + Autoprefixer** – Za automatsku kompatibilnost CSS koda sa različitim browserima.

### 📦 Ostalo

- **lucide-react** (`v0.445.0`) – Ikonice korištene za UI.

> Projekat koristi **ES module sistem** (`"type": "module"`) i organizovan je kao **Vite aplikacija** sa `dev`, `build` i `preview` skriptama.

## Struktura projekta

Ispod se nalazi prikaz direktorijske strukture aplikacije **Moodflix** sa kratkim opisom svakog direktorija i fajla.

moodflix/
├── public/ # Javne datoteke (favicon, index.html, itd.)
├── src/ # Glavni izvorni kod aplikacije
│ ├── assets/ # Slike, ikone i drugi medijski fajlovi
│ │ └── react.svg
│ ├── common/ # Zajedničke varijable i konstante
│ │ └── constants.js
│ ├── components/ # Reusable komponente po sekcijama
│ │ ├── Footer/
│ │ │ └── Footer.jsx
│ │ ├── Hero/
│ │ │ └── Hero.jsx
│ │ ├── Movie/
│ │ │ ├── Movie.jsx
│ │ │ └── MovieList.jsx
│ │ └── Navbar/
│ │ └── Navbar.jsx
│ ├── pages/ # Glavne stranice aplikacije
│ │ ├── Home.jsx
│ │ └── MovieList.jsx
│ ├── App.jsx # Root komponenta aplikacije
│ ├── main.jsx # Ulazna tačka aplikacije
│ └── index.css # Globalni CSS
├── .gitignore
├── index.html # Glavni HTML fajl
├── package.json # Konfiguracija paketa i zavisnosti
├── postcss.config.js
├── tailwind.config.js # Tailwind konfiguracija
├── vite.config.js # Vite konfiguracija
└── README.md

> Ova struktura omogućava jednostavno upravljanje komponentama i proširivanje aplikacije po potrebi. Svaka sekcija (npr. `Movie`, `Navbar`) ima svoju mapu za bolje razdvajanje logike i stilova.

## Funkcionalnosti aplikacije

Aplikacija **Moodflix** omogućava korisnicima da dobiju preporuke za filmove na osnovu svog trenutnog raspoloženja. Fokus je na jednostavnom korisničkom iskustvu i osnovnim principima React razvoja.

### 🎭 1. Odabir raspoloženja

- Na početnoj stranici korisnik bira jedno od ponuđenih raspoloženja:
  - 😊 Happy
  - 😢 Sad
  - 😎 Excited
  - 😌 Relaxed
  - 😠 Angry
  - 🤔 Thoughtful
- Svako dugme poziva funkciju koja postavlja trenutno stanje (`mood`) u aplikaciji.

### 🎬 2. Prikaz preporučenih filmova

- Na osnovu odabranog raspoloženja, aplikacija prikazuje listu relevantnih filmova.
- Filmovi su prikazani sa:
  - Naslovnicom (poster)
  - Nazivom filma
- Podaci mogu biti:
  - Predefinisani u aplikaciji (`constants.js`)
  - Ili dohvaćeni iz vanjskog API-ja (npr. TMDB API)

### 🔄 3. Promjena raspoloženja

- Korisnik može kliknuti na dugme `Change Mood` u navigaciji kako bi se vratio na početni ekran i izabrao novo raspoloženje.

### ✅ Ostale funkcionalnosti

- Navigacija kroz komponente putem **React Router-a**
- Reaktivan interfejs sa **Tailwind CSS**
- Modularna struktura i organizacija komponenti

## Glavne komponente i objašnjenja

U nastavku su objašnjene ključne React komponente koje čine aplikaciju Moodflix. Svaka komponenta ima jasno definisanu odgovornost u okviru UI/UX-a.

### 🧠 `Hero.jsx`

- Prikazuje glavni ekran za odabir raspoloženja.
- Sadrži dugmad za svako dostupno raspoloženje.
- Kada se klikne na dugme, stanje `mood` se postavlja u aplikaciji i korisnik se preusmjerava na listu filmova.

### 🎬 `Movie.jsx`

- Predstavlja jednu filmsku karticu.
- Prikazuje naslovnicu/poster i naziv filma.
- Koristi se unutar `MovieList.jsx` za prikaz više filmova.

### 🎞️ `MovieList.jsx`

- Prikazuje listu svih filmova za izabrano raspoloženje.
- Prikuplja podatke iz `constants.js` (ili iz API-ja ako se koristi).
- Koristi `.map()` da renderuje više `Movie` komponenti.

### 🧭 `Navbar.jsx`

- Prikazuje vrh stranice sa nazivom aplikacije i linkom za povratak na početni ekran ("Change Mood").
- Koristi `Link` iz `react-router-dom` za navigaciju.

### 🏠 `Home.jsx`

- Glavna početna stranica aplikacije.
- Sadrži `Hero` komponentu i logiku za postavljanje raspoloženja.

### 📄 `App.jsx`

- Root komponenta aplikacije.
- Sadrži `BrowserRouter` i definiše sve rute (`/`, `/movies`).
- Omogućava prikaz različitih stranica na osnovu URL-a.

### 📄 `constants.js`

- Sadrži statičke podatke o filmovima grupisane po raspoloženju.
- Na primjer:

```js
export const moviesByMood = {
  happy: [...],
  sad: [...],
  // itd.
};

## 🔧 Moguća poboljšanja (Future improvements)

Moodflix je zamišljen kao jednostavna edukativna aplikacija, ali postoji mnogo prostora za dodatne funkcionalnosti i proširenja. U nastavku su predložena moguća poboljšanja koja bi unaprijedila korisničko iskustvo i funkcionalnost aplikacije.

### 🌐 1. Integracija sa TMDB API
- Umjesto statičkih podataka, koristiti pravi **TMDB API** za dohvat filmova prema žanru, raspoloženju ili popularnosti.
- Omogućiti prikaz dodatnih informacija kao što su opis filma, ocjena, datum izlaska itd.

### 📱 2. Responsive dizajn i mobilna optimizacija
- Podesiti aplikaciju da izgleda odlično i na mobilnim uređajima koristeći Tailwind breakpoint-e.

### 🎭 3. Više raspoloženja i prilagodba korisniku
- Dodati dodatna raspoloženja ili omogućiti korisniku da unese vlastito raspoloženje.
- Na osnovu toga prikazivati filmove koristeći sentiment analizu ili NLP.

### 📄 4. Detaljna stranica filma
- Omogućiti klik na film koji vodi na posebnu stranicu sa detaljima o filmu (sinopsis, trailer, glumačka postava itd.).

### 💾 5. Čuvanje historije i favorita
- Dodati mogućnost da korisnik sačuva omiljene filmove.
- Implementirati LocalStorage ili backend za pohranu istorije gledanja i preferencija.

### 🎨 6. Animacije i interaktivnost
- Dodati lagane animacije pri prelasku između raspoloženja i učitavanja filmova za bolje korisničko iskustvo.

## ✅ Zaključak

Moodflix je jednostavna, ali efektna React aplikacija koja demonstrira kako frontend logika može biti povezana s korisničkim emocijama da bi se kreiralo korisničko iskustvo.

Kroz ovaj projekat obrađene su osnovne teme razvoja modernih web aplikacija:
- upravljanje stanjima i navigacijom pomoću React-a,
- modularna organizacija komponenti,
- osnovna upotreba eksternih podataka (statičkih ili API),
- i stilizacija koristeći Tailwind CSS.

Ovaj projekat može poslužiti kao osnova za složenije aplikacije koje uključuju rad s API-jem, korisničke sesije, autentifikaciju, i naprednu logiku preporuka.

> Moodflix nije samo tehnički demo, već i prilika da se razumije kako male ideje mogu imati velik edukativni potencijal.

---

📁 **Repozitorij**: [https://github.com/kaizerpwn/moodflix]
```
