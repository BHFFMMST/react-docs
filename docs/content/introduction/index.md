# Introduction to Web Development and Version Control System

## Šta je web development?

Web development je proces pravljenja i održavanja web stranica i aplikacija. Dakle, sve što radite na internetu – bilo da čitate vijesti, gledate YouTube, kupujete nešto online ili provjeravate raspored predavanja – sve to je rezultat web developmenta.

Tu razlikujemo dva velika dijela:

🔹 1. Frontend (klijentska strana)

Frontend je sve ono što korisnik vidi i koristi – izgled stranice, dugmad, slike, boje, meni, tekst… To je vizuelni dio aplikacije.

Tehnologije koje se koriste u frontendu su:

HTML – pravi strukturu stranice. Zamislite HTML kao kostur web stranice – određuje gdje ide naslov, paragraf, dugme, slika.

CSS – daje stil i ljepotu toj strukturi. CSS određuje boje, raspored, fontove, margine. On uređuje kako stranica izgleda.

JavaScript – daje stranici život. On omogućava da nešto reaguje kada kliknemo dugme, da se prikazuje/skriva sadržaj, da se automatski računa neka vrijednost.

-----------------------------------------------------------------------------------
# 2. Backend (serverska strana)

S druge strane imamo backend – to je nevidljivi dio, koji korisnik ne vidi, ali bez kojeg ništa ne bi funkcionisalo.

Backend se brine o:

-prijavi korisnika,

-spremanju podataka (npr. proizvoda, korisničkih računa),

-komunikaciji s bazom podataka,

-sigurnosti podataka.

Tehnologije koje se tu koriste su: Node.js, Python, PHP, Java, te baze podataka kao MySQL, MongoDB i drugi.

--------------------------------------------------------------------------------------------
# Kako frontend i backend sarađuju?

Frontend šalje zahtjev – npr. “Daj mi korisničke podatke”

Backend provjerava bazu i vraća te podatke

Frontend ih prikazuje korisniku

## Šta je React.js?

React je moderna JavaScript biblioteka koju je razvio Facebook.

Služi za kreiranje korisničkog interfejsa (UI), ali na efikasniji i modularniji način.

Zamislite web aplikaciju kao LEGO kuću:

Svaka LEGO kockica je komponenta – dugme, kartica, meni, forma.

Komponente možemo više puta koristiti i kombinovati bez da svaki put pišemo sve ispočetka.

React omogućava da aplikaciju gradimo iz tih malih, ponovo iskoristivih dijelova, što je savršeno za velike i kompleksne projekte.


## Kreiranje React projekta pomoću Vite-a 


Kako uopšte pravimo React aplikaciju?

Nekada smo koristili alat koji se zvao Create React App (CRA). Međutim, danas postoji brži i lakši alat – Vite.

🔹 Šta je Vite?

Vite (čita se: vit) je moderni build alat koji nam pomaže da brzo postavimo React aplikaciju.

Koristi nove tehnologije u pozadini (kao što je ESM – ECMAScript Modules).

Mnogo je brži od starog CRA-a, naročito kada radimo lokalno u razvoju.

📌 Zamislite Vite kao alat koji umjesto nas postavlja sav osnovni React kod i folder strukturu – tako da ne moramo pisati sve od nule.

🔹 Priprema: Instalacija Node.js

Da bismo koristili Vite i React, prvo moramo imati Node.js instaliran.

🔧 Node.js je program koji nam omogućava da u komandnoj liniji pokrećemo JavaScript i upravljamo projektima.

✅ Kada instaliramo Node.js, automatski dobijamo i npm – to je alat koji nam omogućava instalaciju React-a i drugih paketa.


📥 Koraci:

Otvorimo https://nodejs.org

Skinemo verziju označenu kao "LTS" (Long Term Support)

Instaliramo je klikom "Next → Next" kao i bilo koji drugi program



## Kreiranje projekta pomoću Vite-a

Nakon što imamo Node.js, otvaramo terminal (ili VS Code terminal) i kucamo sljedeće komande:

npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev

Šta ove komande rade?

npm create vite@latest my-react-app → kaže: napravi novi projekat koristeći Vite, pod nazivom my-react-app, i neka koristi React kao šablon

cd my-react-app → ulazimo u naš novi folder s projektom

npm install → instaliramo sve zavisnosti (biblioteke koje su potrebne za rad)

npm run dev → pokrećemo razvojni server, i aplikacija se otvara u browseru

🖥️ Nakon npm run dev, terminal nam da lokalni link, npr. http://localhost:5173, koji otvorimo u browseru i odmah vidimo početnu React stranicu.

# Otvaranje projekta u VS Code

Ako koristimo Visual Studio Code, projekat možemo otvoriti ovako:

code .


To će otvoriti trenutni folder u VS Code-u, i možemo odmah početi uređivati kod.

📌 Ako ova komanda ne radi, možda treba dodati VS Code u PATH tokom instalacije – to se može naknadno uključiti.

## Pitanja i dodatni savjeti

Ako dobijete grešku tokom instalacije: provjerite da li imate Node.js i da li ste u pravom folderu.

Ako je npm run dev uspio, to znači da sve radi i spremni ste da počnete s uređivanjem aplikacije.



# 📁 Struktura React projekta (Vite) – Objašnjenje

 Kada smo uspješno pokrenuli React aplikaciju pomoću Vite-a, hajde da zajedno pogledamo šta smo to zapravo dobili u projektu i čemu šta služi.

## 📁 1. node_modules/

Ovo je folder koji sadrži sve biblioteke i pakete koje je naš projekat instalirao pomoću npm install.

Ne diramo ga ručno!

Automatski se kreira.

Zato se dodaje u .gitignore kako ne bi išao na GitHub jer je ogroman.

## 📁 2. public/

Ovaj folder sadrži staticke fajlove koji se ne obrađuju od strane React-a. Sve što stavimo ovdje biće dostupno direktno u browseru.

Npr. slike, favicon (ikonica stranice), dokumenti.

📌 Primjer: ako ovdje dodamo fajl logo.png, možemo mu pristupiti putem URL-a: http://localhost:5173/logo.png.

## 📄 3. index.html

Ovo je HTML šablon naše aplikacije. Iako radimo s React-om (koji koristi JavaScript), cijela aplikacija se ipak “uliva” u ovaj jedan HTML fajl.

🔍 Pogledaj liniju:

<div id="root"></div>


→ React ubacuje kompletan sadržaj aplikacije unutar ovog div elementa. To se dešava u fajlu main.jsx.

🎤 “Iako ne pišemo puno HTML-a direktno ovdje, ovaj fajl je ključan jer predstavlja osnovu aplikacije.”

## 📁 4. src/ – Najvažniji folder

Ovdje se nalazi sav naš React kod. To je mjesto gdje pišemo komponente, stilove, logiku aplikacije.

## 📄 main.jsx

Ovo je ulazna tačka aplikacije. Ovdje React povezuje App.jsx sa index.html.

U kodu obično vidimo:

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);


To znači: uzmi <App /> komponentu i ubaci je u div koji ima id="root" – upravo onaj u index.html.

## 📄 App.jsx

Ovo je glavna komponenta aplikacije – možemo je zamisliti kao srce svega.

Ovdje prikazujemo sve ostale komponente: navigaciju, kartice, forme, itd.

Svaki novi dio koji pravimo, na kraju uđe ovdje.

Svaki React projekat ima App kao centralni prikaz, a ostale komponente dodajemo i prikazujemo unutar njega.

## 📁 assets/

Folder za slike, ikone, stilove koje koristimo u aplikaciji. Na slici vidimo npr. react.svg – to je logo koji se pojavljuje na početnoj stranici aplikacije.

## 📄 App.css i index.css

App.css – stilovi koji se odnose na App.jsx komponentu.

index.css – globalni stilovi koji važe za cijelu aplikaciju.

Možemo ih uređivati, dodavati svoje klase i praviti svoj dizajn.


# 📄 Ostali važni fajlovi

## 📄 .gitignore

Ovdje pišemo koje fajlove i foldere ne želimo da šaljemo na GitHub. Na primjer:

node_modules
dist
.env

## 📄 package.json

Vrlo važan fajl. On sadrži:

-naziv aplikacije

-sve instalirane biblioteke (dependencies)

-skripte koje možemo pokretati (npr. npm run dev)

-verziju projekta

Ukoliko želite da vidite šta je instalirano u projektu, samo otvorite ovaj fajl i pogledajte dio dependencies.

## 📄 vite.config.js

Konfiguracija za Vite alat. Nećemo ga puno dirati za osnovne projekte, ali kad budemo radili naprednije stvari kao aliasi, proxy, pluginovi – ovo je mjesto gdje se sve podešava.

## 📄 README.md

Tekstualni fajl u kojem možemo napisati osnovne informacije o projektu. Na GitHub-u se on prikazuje automatski na početnoj stranici repozitorija.


# Git i GitHub – Osnove verzionisanja

## Šta je Git?

Git je verzioni sistem – alat koji pamti svaku promjenu koju napravimo u projektu.

Zamislite ga kao vremensku mašinu:

Svaka promjena koju napravimo se zabilježi kao snapshot.

Možemo se vratiti unazad, vidjeti ko je šta promijenio, kada, i zašto.

Idealno za timski rad – više ljudi može raditi istovremeno, a da se ne pregazi kod.

📌 Git omogućava programerima da znaju:

✅ Ko je napravio promjenu

✅ Kada je napravljena

✅ Šta je tačno promijenjeno

✅ Zašto je promjena uvedena (kroz opis – commit message)


## 🔹 Šta je GitHub?

GitHub je online platforma koja čuva Git projekte u cloud-u.

Tu pohranjujemo svoj kod i dijelimo ga s drugima

Možemo raditi u timovima, otvarati zadatke (issues), praviti grane (branches), recenzirati kod (pull requests)


## Kako Git funkcioniše?

Zamislimo da radimo na dokumentu:

Kada napišemo dio koda, pripremimo ga za snimanje (git add)

Onda snimimo promjenu s opisom (git commit)

I po želji pošaljemo to na GitHub (git push)

Git čuva istoriju svake te promjene u obliku commit-a, a svi commit-i zajedno čine istoriju projekta.

## 📄 Glavne komande u Git-u
Komanda	                    Šta radi
git init	                  Inicijalizuje prazan Git repozitorij
git add .	                  Priprema sve fajlove za commit
git commit -m "opis"	      Snima promjene sa porukom
git status	                Prikazuje trenutno stanje fajlova
git clone <url>	            Klonira GitHub repozitorij na računar
git branch	                Prikazuje (ili pravi) grane
git merge	                  Spaja promjene iz druge grane
git pull	                  Preuzima promjene s GitHub-a
git push	                  Šalje promjene na GitHub


## Branching (grane)

Svaka grana je paralelna linija razvoja.

main je glavna verzija.

Možemo napraviti grane za testiranje, nove funkcije, ispravke grešaka itd.

git branch nova-funkcija
git checkout nova-funkcija


Branching je kao da pravite kopiju projekta da biste eksperimentisali bez straha da nešto pokvarite.

## Commit snapshoti

Svaki commit je kao fotografija trenutnog stanja projekta. Zahvaljujući tome možemo:

-Vratiti se na bilo koji prethodni commit

-Pratiti promjene po datumu i autoru

-Pregledati historiju promjena

## GitHub u praksi

Kreiramo repozitorij na GitHub-u (bez README ako već imamo fajlove)

Na računaru koristimo:

git init
git remote add origin https://github.com/ime/repo.git
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main

Nakon toga, sve naredne promjene pratimo i šaljemo pomoću add → commit → push.

## Pull Request i saradnja

Kada radimo u timu, pravimo granu i tražimo odobrenje putem Pull Requesta.

Tu tim može:

dodati komentare,

zatražiti izmjene,

spojiti promjene u main.


# Praktična Git i GitHub vježba

🎯 Cilj: Naučiti kako se kreira Git repozitorij, kako se prate promjene, i kako se sve šalje na GitHub.

🔹 1. Inicijalizacija Git repozitorija

U VS Code terminalu (ili običnom terminalu) kucati:

git init


📝 Ovo kreira .git folder i omogućava Git-u da prati promjene u ovom projektu.

🔹 2. Dodavanje fajlova za praćenje
git add .


📌 Ova komanda dodaje sve fajlove u tzv. “staging area” – znači priprema ih za snimanje.

Ako želimo samo jedan fajl: git add imeFajla.ext

🔹 3. Kreiranje prvog commita
git commit -m "Initial commit"


Ovim čuvamo stanje projekta s opisom. Poželjno je da opis bude kratak i jasan.

## 4. Kreiranje GitHub repozitorija

➡️ Otići na https://github.com

➡️ Kliknuti New Repository
➡️ Nazvati ga npr. my-first-react-app
➡️ Ne dodavati README jer ga već imamo lokalno
➡️ Kliknuti Create repository

## 5. Povezivanje lokalnog repozitorija sa GitHub-om
git remote add origin https://github.com/korisnickoime/my-first-react-app.git

## 6. Postavljanje glavne grane (main)
git branch -M main

## 7. Slanje koda na GitHub
git push -u origin main


 Ako se traži username i password, korisnici treba da koriste GitHub token umjesto lozinke (može se generisati iz GitHub Settings > Developer Settings > Tokens).


Otvoriti GitHub repozitorij – učesnici će sada vidjeti svoj kod online!


## Dodatni zadaci za samostalan rad

Napravi novu granu:

git checkout -b nova-funkcija


Uredi jedan fajl i commitaj promjenu:

git add .
git commit -m "Dodana nova funkcija"


Vrati se na main i spoji promjene (napredno):

git checkout main
git merge nova-funkcija

-----------------------------------------------------------------------------------------------------------------------------------
# Q&A i Zajednički problemi 


## 1. Šta ako zaboravimo git add?

 Problem:
Napravili ste izmjenu u fajlu, uradili git commit, ali promjena nije snimljena.

Objašnjenje:
Git može da commit-uje samo ono što je prethodno dodano sa git add. Ako to preskočimo, promjene ostaju „nevidljive“ za Git.

Rješenje:

Provjerite stanje:

git status


Vidjet ćete koji su fajlovi izmijenjeni, ali nisu „staged“.

Dodajte ih i uradite commit:

git add naziv_fajla
git commit -m "Dodaj pravi opis"


 Savjet: uvijek koristite git status prije commita da provjerite šta je dodano.

## 2. Kako vratiti stariju verziju fajla?
a) Vratiti fajl na stanje iz zadnjeg commit-a:

Ako želite odbaciti lokalne promjene:

git restore naziv_fajla


Ova komanda će izbrisati sve izmjene u fajlu i vratiti ga na posljednju verziju iz repozitorija.

b) Vratiti cijeli projekat na raniji commit:

Pronađi ID commita:

git log


Vrati se na željeni commit (privremeno):

git checkout <commit_id>


 Napomena: ovo vas stavlja u „detached HEAD“ mod, što znači da gledate staru verziju i da ne treba praviti nove promjene direktno u tom stanju.

Ako želiš da napraviš novu granu iz tog stanja:

git checkout -b fix-old-version

## 3. Kako se kreira .gitignore?

 .gitignore je fajl u koji pišemo imena fajlova i foldera koje ne želimo da Git prati.

 Najčešće se koristi da ignorišemo:

node_modules/

dist/

.env

privremene .log fajlove

Kako ga napraviti:

U korijenu projekta klikni New File

Nazovi ga .gitignore (bez ekstenzije)

U njega upiši:

node_modules/
dist/
.env
*.log


Git će automatski ignorisati sve što je tu navedeno.

Ovo je korisno da ne šaljemo stvari koje ne trebaju biti na GitHub-u – kao što su ogromni folderi, lokalne konfiguracije ili tajni podaci.

