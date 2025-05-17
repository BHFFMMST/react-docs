React Data Manipulation: Upravljanje Podacima u React Aplikacijama

Uvod u Upravljanje Podacima u Reactu
Što je React Data Manipulation?
React Data Manipulation odnosi se na tehnike i mehanizme za upravljanje podacima u React aplikacijama. To uključuje:

Dohvaćanje podataka iz vanjskih izvora (API, baze podataka)
Transformaciju i obradku podataka
Upravljanje lokalnim stanjem aplikacije
Prijenos podataka između komponenata
Optimizaciju performansi pri radu s podacima

Zašto je Važno Pravilno Upravljati Podacima?
✔️ Predvidljivo ponašanje aplikacije
✔️ Lakše održavanje koda
✔️ Bolje performanse
✔️ Smanjenje grešaka
✔️ Poboljšano korisničko iskustvo

Osnove Upravljanja Podacima
Lokalno Stanje (Local State)
Najosnovniji oblik upravljanja podacima u Reactu je korištenje lokalnog stanja komponente.

import { useState } from 'react';

function Brojac() {
  const [count, setCount] = useState(0); // Inicijalna vrijednost 0

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

