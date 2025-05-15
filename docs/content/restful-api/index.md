# APIs and RESTful services

## Uvod
RESTful API-ji su ključna komponenta u modernom web razvoju. Oni omogućavaju komunikaciju između različitih aplikacija putem interneta.
REST (što je skraćenica za Representational State Transfer) API-ji funkcionišu na bestatusnoj klijent-server arhitekturi, pružajući standardizovan način za kreiranje, čitanje, ažuriranje i brisanje resursa.
Integracija RESTful API-ja sa Reactom unapređuje funkcionalnost vaših web aplikacija omogućavajući im da dinamički dohvaćaju i ažuriraju podatke. Ova integracija olakšava besprijekorno korisničko iskustvo, osiguravajući da aplikacija ostane responzivna i ažurna.
U ovom dijelu ćemo se posvetiti osnovama RESTful API-ja i provesti vas kroz proces rada s njima u Reactu. Od postavljanja novog React projekta do rukovanja CRUD operacijama i implementacije autentifikacije, steći ćete sveobuhvatno razumijevanje integracije API-ja u vaše React aplikacije.

## Razumijevanje RESTful API-ja
### Šta je REST?
REST (Representational State Transfer) je arhitektonski stil koji definiše skup ograničenja koja se koriste prilikom kreiranja web servisa. To nije protokol, već skup principa koji diktiraju kako bi se web servisi trebali ponašati.
U svojoj srži, REST se oslanja na bestatusni klijent-server komunikacijski model, što znači da svaki zahtjev od klijenta sadrži sve informacije potrebne za razumijevanje i obradu tog zahtjeva.

### Ključni principi REST-a
RESTful API-ji slijede nekoliko ključnih principa, uključujući bestatusnost, uniformni interfejs i interakcije zasnovane na resursima.
Bestatusnost osigurava da je svaki zahtjev od klijenta prema serveru nezavisan i da server ne pohranjuje nikakve informacije o stanju klijenta između zahtjeva. Princip uniformnog interfejsa definiše standardizovan način interakcije s resursima, promovišući jednostavnost i dosljednost.

### Anatomija RESTful API-ja
RESTful API se sastoji od resursa, od kojih je svaki identifikovan jedinstvenim URI-jem (Uniform Resource Identifier). Ovi resursi se mogu manipulisati koristeći standardne HTTP metode kao što su GET, POST, PUT, PATCH i DELETE. Odgovori API-ja obično uključuju podatke u formatu kao što je JSON (JavaScript Object Notation) ili XML (eXtensible Markup Language).

### Krajnje tačke RESTful API-ja
Krajnje tačke su specifični URL-ovi koji predstavljaju resurse koje izlaže RESTful API. Na primjer, jednostavan blog API mogao bi imati krajnje tačke poput `/posts` za dohvaćanje svih blog objava i `/posts/{id}` za dohvaćanje specifične objave prema njenom jedinstvenom identifikatoru.
Razumijevanje ovih krajnjih tačaka je ključno prilikom rada s RESTful API-jima u Reactu, jer one definišu podatke kojima možete pristupiti i manipulisati.

## Kako uputiti API zahtjeve u React-u
### Fetch API
Fetch API je moderni interfejs za upućivanje HTTP zahtjeva u pregledniku. Pruža moćniji i fleksibilniji način rukovanja mrežnim zahtjevima u poređenju sa starijim tehnikama poput XMLHttpRequest.

```javascript
// src/components/ApiExample.js
import React, { useState, useEffect } from 'react';

const ApiExample = () => {
  const [data, setData] = useState([]);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/posts');
        const result = await response.json();
        setData(result);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };
    fetchData();
  }, []);

  return (
    <div>
      <h1>API Data</h1>
      <ul>
        {data.map((item) => (
          <li key={item.id}>{item.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default ApiExample;
```

U ovom primjeru, `useEffect` hook se koristi za dohvaćanje podataka kada se komponenta montira. Funkcija fetch se koristi za upućivanje GET zahtjeva na specificiranu API krajnju tačku ('https://api.example.com/posts'), a odgovor se konvertuje u JSON koristeći `response.json()`.

### Slanje GET zahtjeva
Prilikom rada s RESTful API-jima, GET zahtjevi su najčešći. Oni dohvaćaju podatke sa servera bez da ih mijenjaju. Hajde da poboljšamo naš primjer tako da uključi upitne parametre i obradi različite aspekte GET zahtjeva.

```javascript
// src/components/ApiExample.js

// ... (previous imports)

const ApiExample = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState

(true);

  useEffect(() => {
    const fetchData = async () => {
      try {
        // Simulating a delay to show loading state
        setTimeout(async () => {
          const response = await fetch('https://api.example.com/posts?userId=1');
          const result = await response.json();
          setData(result);
          setLoading(false);
        }, 1000);
      } catch (error) {
        console.error('Error fetching data:', error);
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      <h1>API Data</h1>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default ApiExample;
```
U ovom primjeru, uvodi se stanje učitavanja kako bi se korisnicima pružila povratna informacija dok se podaci dohvaćaju. Stanje `loading` se inicijalno postavlja na `true` i mijenja na `false` kada se podaci dohvate.

### Rukovanje asinhronim operacijama sa `async/await`
Upotreba `async/await` sintakse čini asinhroni kod čitljivijim i lakšim za rad. Omogućava vam da pišete asinhroni kod koji izgleda i ponaša se slično sinhronom kodu.

```javascript
// src/components/ApiExample.js

// ... (previous imports)

const ApiExample = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/posts?userId=1');
        const result = await response.json();
        setData(result);
        setLoading(false);
      } catch (error) {
        console.error('Error fetching data:', error);
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      <h1>API Data</h1>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default ApiExample;
```

Ovdje je funkcija `fetchData` deklarisana kao asinhrona funkcija koristeći ključnu riječ `async`. Ovo omogućava upotrebu `await` unutar funkcije, čineći asinhroni kod jednostavnijim i održavajući čistu i čitljivu strukturu.

### Obrada grešaka
Ključno je elegantno obraditi greške prilikom slanja API zahtjeva. U prethodnim primjerima, uveli smo osnovni mehanizam za obradu grešaka koristeći `try/catch` blokove. Proširimo ovo kako bismo pružili detaljnije poruke o greškama.

```javascript
// src/components/ApiExample.js

// ... (previous imports)

const ApiExample = () => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/posts?userId=1');

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const result = await response.json();
        setData(result);
        setLoading(false);
      } catch (error) {
        console.error('Error fetching data:', error);
        setError('An error occurred while fetching the data. Please try again later.');
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      <h1>API Data</h1>
      {loading ? (
        <p>Loading...</p>
      ) : error ? (
        <p>{error}</p>
      ) : (
        <ul>
          {data.map((item) => (
            <li key={item.id}>{item.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default ApiExample;
```

U ovom primjeru, provjerava se svojstvo `response.ok` kako bi se utvrdilo da li je HTTP zahtjev bio uspješan. Ako nije, baca se greška s informacijama o HTTP statusu. Dodatno, postavlja se korisniku prikladnija poruka o grešci u stanju `error` i ona se prikazuje u komponenti.

## Kako prikazati API podatke u React komponentama
### Stanje i propertiji (props) u React-u
U Reactu, komponente upravljaju svojim unutrašnjim stanjem, što im omogućava da se dinamički ažuriraju i ponovo renderuju na osnovu promjena. Properti (props), s druge strane, se koriste za prosljeđivanje podataka od roditeljskih ka dječijim komponentama.
Hajde da razumijemo kako koristiti stanje i propertije za prikaz API podataka.
```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

const DisplayData = () => {
  const [apiData, setApiData] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get('https://api.example.com/data');
        setApiData(response.data);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    fetchData();
  }, []);

  return (
    <div>
      <h2>API Data Display</h2>
      {apiData ? (
        // Render your component using the fetched data
        <MyComponent data={apiData} />
      ) : (
        // Render a loading state or placeholder
        <p>Loading...</p>
      )}
    </div>
  );
};

const MyComponent = ({ data }) => {
  return (
    <div>
      <p>{data.message}</p>
      {/* Render other components based on data */}
    </div>
  );
};

export default DisplayData;
```

### Ažuriranje stanja sa preuzetim podacima
Kada se podaci uspješno preuzmu sa API-ja, mi ažuriramo stanje komponente koristeći `setApiData(response.data)`. Ovo pokreće ponovno renderovanje, osiguravajući da korisničko sučelje odražava najnovije informacije.

### Dinamičko renderovanje podataka
Prosljeđivanje podataka kao propertija (props) omogućava komponentama da dinamički renderuju sadržaj. U primjeru, `MyComponent` prima podatke kao prop i renderuje sadržaj na osnovu tih podataka.

### Stanja učitavanja i obrada grešaka
Prikazivanje stanja učitavanja (`<p>Učitavanje...</p>`) dok se čeka na API podatke osigurava bolje korisničko iskustvo. Dodatno, uključili smo obradu grešaka kako bismo uhvatili i zabilježili sve probleme koji mogu nastati tokom API zahtjeva.

## CRUD operacije sa RESTful API-jima
### Kreiranje podataka (POST zahtjevi)
Kreiranje podataka uključuje slanje POST zahtjeva API-ju. Implementirajmo jednostavnu formu za dodavanje novih stavki.

```javascript
import React, { useState } from 'react';
import axios from 'axios';

const CreateData = () => {
  const [newData, setNewData] = useState('');

  const handleCreate = async () => {
    try {
      await axios.post('https://api.example.com/data', { newData });
      alert('Data created successfully!');
      // Optionally, fetch and update the displayed data
    } catch (error) {
      console.error('Error creating data:', error);
    }
  };

  return (
    <div>
      <h2>Create New Data</h2>
      <input
        type="text"
        value={newData}
        onChange={(e) => setNewData(e.target.value)}
      />
      <button onClick={handleCreate}>Create</button>
    </div>
  );
};

export default CreateData;
```
U ovom primjeru, hvatamo korisnički unos pomoću `useState` hooka i šaljemo POST zahtjev API-ju kada se klikne na dugme "Kreiraj".

### Čitanje podataka (GET zahtjevi)
Čitanje podataka uključuje slanje GET zahtjeva za dohvaćanje informacija sa API-ja. Ovo smo već obradili u prethodnom odjeljku o prikazivanju API podataka.

### Ažuriranje podataka (PUT/PATCH zahtjevi)
Ažuriranje podataka zahtijeva slanje PUT ili PATCH zahtjeva API-ju sa izmijenjenim podacima. Kreirajmo primjer za ažuriranje postojećih podataka.

```javascript
import React, { useState } from 'react';
import axios from 'axios';

const UpdateData = () => {
  const [updatedData, setUpdatedData] = useState('');

  const handleUpdate = async () => {
    try {
      await axios.put('https://api.example.com/data/1', { updatedData });
      alert('Data updated successfully!');
      // Optionally, fetch and update the displayed data
    } catch (error) {
      console.error('Error updating data:', error);
    }
  };

  return (
    <div>
      <h2>Update Data</h2>
      <input
        type="text"
        value={updatedData}
        onChange={(e) => setUpdatedData(e.target.value)}
      />
      <button onClick={handleUpdate}>Update</button>
    </div>
  );
};

export default UpdateData;
```

U ovom primjeru, hvatamo ažurirane podatke i šaljemo PUT zahtjev na API krajnju tačku za specifičnu stavku.

### Brisanje podataka (DELETE zahtjevi)
Brisanje podataka uključuje slanje DELETE zahtjeva API-ju. Evo primjera kako implementirati funkcionalnost brisanja.

```javascript
import React from 'react';
import axios from 'axios';

const DeleteData = () => {
  const handleDelete = async () => {
    try {
      await axios.delete('https://api.example.com/data/1');
      alert('Data deleted successfully!');
      // Optionally, fetch and update the displayed data
    } catch (error) {
      console.error('Error deleting data:', error);
    }
  };

  return (
    <div>
      <h2>Delete Data</h2>
      <button onClick={handleDelete}>Delete</button>
    </div>
  );
};

export default DeleteData;
```

U ovom primjeru, klik na dugme "Izbriši" pokreće DELETE zahtjev prema API-ju, uklanjajući specificiranu stavku.

## Kako rukovati formama i korisničkim unosom?
### Kontrolisane komponente
Reactove kontrolisane komponente omogućavaju nam da dinamički rukujemo unosom u forme. Vrijednost unosa je kontrolisana stanjem komponente.

```javascript
import React, { useState } from 'react';

const ControlledComponent = () => {
  const [inputValue, setInputValue] = useState('');

  return (
    <div>
      <h2>Controlled Component</h2>
      <input
        type="text"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)}
      />
      <p>Input Value: {inputValue}</p>
    </div>
  );
};

export default ControlledComponent;
```

### Podnošenje forme i rukovanje njime
Forme u Reactu mogu se podnijeti rukovanjem `onSubmit` eventom. Kreirajmo jednostavan primjer podnošenja forme.

```javascript
import React, { useState } from 'react';

const FormSubmission = () => {
  const [formData, setFormData] = useState({
    username: '',
    password: '',
  });

  const handleInputChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value,
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // Perform form submission logic, e.g., send data to API
  };

  return (
    <div>
      <h2>Form Submission</h2>
      <form onSubmit={handleSubmit}>
        <label>
          Username:
          <input
            type="text"
            name="username"
            value={formData.username}
            onChange={handleInputChange}
          />
        </label>
        <label>
          Password:
          <input
            type="

password"
            name="password"
            value={formData.password}
            onChange={handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};

export default FormSubmission;
```

U ovom primjeru, funkcija `handleInputChange` ažurira podatke forme u stanju komponente, a funkcija `handleSubmit` sprječava podrazumijevano podnošenje forme i omogućava vam da izvršite prilagođenu logiku, kao što je slanje podataka API-ju.

### Slanje podataka API-ju
Da biste poslali podatke API-ju, integrišite logiku podnošenja forme sa vašim kodom za HTTP zahtjeve. Koristite odgovarajuću HTTP metodu (na primjer, POST) za kreiranje novih podataka.

### Validacija i poruke o greškama
Implementacija validacije forme je ključna za osiguravanje integriteta podataka. Možete koristiti uslovno renderovanje za prikazivanje poruka o greškama na osnovu pravila validacije.

```javascript
import React, { useState } from 'react';

const FormValidation = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!username || !password) {
      setError('Username and password are required.');
      return;
    }

    // Perform form submission logic, e.g., send data to API
  };

  return (
    <div>
      <h2>Form Validation</h2>
      {error && <p style={{ color: 'red' }}>{error}</p>}
      <form onSubmit={handleSubmit}>
        <label>
          Username:
          <input
            type="text"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
          />
        </label>
        <label>
          Password:
          <input
            type="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};

export default FormValidation;
```

U ovom primjeru, stanje `error` se koristi za prikazivanje poruke o grešci kada validacija forme ne uspije.

## Autentifikacija i autorizacija
### Razumijevanje razlike između autentifikacije i autorizacije
Autentifikacija provjerava identitet korisnika, dok autorizacija određuje koje radnje korisnik smije izvršiti. Autentifikacija zasnovana na tokenima se obično koristi za osiguravanje API-ja.

### Implementacija autentifikacije zasnovane na tokenima
Da bi se implementirala autentifikacija zasnovana na tokenima, korisnici se obično prijavljuju kako bi dobili pristupni token, koji se zatim šalje sa svakim API zahtjevom za autorizaciju.

```javascript
import React, { useState } from 'react';
import axios from 'axios';

const Authentication = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [token, setToken] = useState('');

  const handleLogin = async () => {
    try {
      const response = await axios.post('https://api.example.com/login', {
        username,
        password,
      });

      setToken(response.data.token);
      // Save the token securely (e.g., in local storage)
    } catch (error) {
      console.error('Login failed:', error);
    }
  };

  const handleLogout = () => {
    setToken('');
    // Clear the saved token
  };

  return (
    <div>
      <h2>Token-based Authentication</h2>
      {token ? (
        <button onClick={handleLogout}>Logout</button>
      ) : (
        <div>
          <label>
            Username:
            <input
              type="text"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
            />
          </label>
          <label>
            Password:
            <input
              type="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
          </label>
          <button onClick={handleLogin}>Login</button>
        </div>
      )}
    </div>
  );
};

export default Authentication;
```

U ovom primjeru, funkcija `handleLogin` šalje POST zahtjev sa korisničkim kredencijalima, i nakon uspjeha, pristupni token se pohranjuje u stanju komponente.

### Osiguravanje API zahtjeva
Da biste osigurali API zahtjeve, uključite pristupni token u zaglavlja zahtjeva. Axios pruža `Authorization` zaglavlje u ovu svrhu.

```javascript
const fetchData = async () => {
  try {
    const response = await axios.get('https://api.example.com/data', {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });
    // Handle the response
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
```

Uključite ovo zaglavlje u sve zahtjeve koji zahtijevaju autentifikaciju.


## Kako optimizirati performanse?
### Keširanje API odgovora
Keširanje API odgovora može značajno poboljšati performanse. Pohranite preuzete podatke u varijablu stanja ili globalno rješenje za upravljanje stanjem kao što je Redux kako biste izbjegli nepotrebne API pozive.

```javascript
const [cachedData, setCachedData] = useState(null);

const fetchData = async () => {
  try {
    if (cachedData) {
      // Use cached data if available
      return;
    }

    const response = await axios.get('https://api.example.com/data');
    setCachedData(response.data);
    // Handle the response
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};
```

### Lijeno učitavanje i peginacija
Možete implementirati lijeno učitavanje i paginaciju kako biste optimizirali renderovanje velikih skupova podataka. Dohvatite samo podatke potrebne za trenutni prikaz i učitajte dodatne podatke dok korisnik skroluje ili navigira.

### Optimizacija ponovnog renderovanja pomoću React.memo
`React.memo` je komponenta višeg reda koja memoriše funkcionalne komponente, sprječavajući nepotrebna ponovna renderovanja ako se propertiji (props) komponente nisu promijenile.

```javascript
import React, { memo } from 'react';

const MemoizedComponent = memo(({ data }) => {
  return (
    <div>
      <p>{data.message}</p>
      {/* Render other components based on data */}
    </div>
  );
});

export default MemoizedComponent;
```
Omotajte komponente sa `React.memo` kako biste optimizirali performanse renderovanja.

## Kako testirati vašu React aplikaciju sa RESTful API-jima?
Testiranje je ključni dio procesa razvoja, osiguravajući da vaša aplikacija radi kako se očekuje i ostaje robusna čak i dok se razvija.
U ovom odjeljku, istražit ćemo različite aspekte testiranja u React aplikaciji koja interaguje sa RESTful API-jima.

### Jedinično testiranje komponenti
Jedinično testiranje je fokusirano na testiranje pojedinačnih jedinica koda u izolaciji. Za React komponente, ovo uključuje testiranje ponašanja komponente, renderovanja i interakcija. Koristit ćemo popularnu biblioteku za testiranje `@testing-library/react` za naše primjere.

Razmotrimo jednostavnu React komponentu koja dohvaća i prikazuje podatke sa RESTful API-ja:

```javascript
// src/components/UserProfile.js

import React, { useState, useEffect } from 'react';
import axios from 'axios';

const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const fetchUser = async () => {
      try {
        const response = await axios.get(`https://api.example.com/users/${userId}`);
        setUser(response.data);
      } catch (error) {
        console.error('Error fetching user data:', error);
      }
    };

    fetchUser();
  }, [userId]);

  return (
    <div>
      {user ? (
        <div>
          <h2>{user.name}</h2>
          <p>Email: {user.email}</p>
        </div>
      ) : (
        <p>Loading user data...</p>
      )}
    </div>
  );
};

export default UserProfile;
```

Sada, kreirajmo jedinični test za ovu komponentu:

```javascript
// src/components/UserProfile.test.js

import React from 'react';
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import UserProfile from './UserProfile';

test('renders user profile data', async () => {
  // Mocking Axios for unit testing
  jest.mock('axios');
  import axios from 'axios';
  axios.get.mockResolvedValue({ data: { name: 'John Doe', email: 'john@example.com' } });

  // Render the component with a mocked userId
  render(<UserProfile userId={1} />);

  // Check if the loading state is displayed initially
  expect(screen.getByText('Loading user data...')).toBeInTheDocument();

  // Wait for the component to render with fetched data
  const nameElement = await screen.findByText('John Doe');
  const emailElement = screen.getByText('Email: john@example.com');

  // Check if the user data is displayed correctly
  expect(nameElement).toBeInTheDocument();
  expect(emailElement).toBeInTheDocument();
});
```

Ovaj jedinični test koristi Jest i `@testing-library/react` kako bi osigurao da UserProfile komponenta ispravno renderuje podatke korisnika. Mi mokiramo Axios biblioteku kako bismo simulirali uspješan API odgovor. Na ovaj način, test se fokusira na ponašanje komponente bez stvarnih mrežnih zahtjeva.

### Mokiranje API zahtjeva za testiranje

Mokiranje API zahtjeva je ključno za izolovanje komponenti i testiranje njihove logike bez oslanjanja na stvarnu mrežnu komunikaciju. U prethodnom primjeru, koristili smo Jestovu funkciju `jest.mock` za mokiranje Axios biblioteke.
Evo još jednog primjera sa složenijom komponentom koja šalje više API zahtjeva:
```javascript
// src/components/PostList.js

import React, { useState, useEffect } from 'react';
import axios from 'axios';

const PostList = () => {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    const fetchPosts = async () => {
      try {
        const response = await axios.get('https://api.example.com/posts');
        setPosts(response.data);
      } catch (error) {
        console.error('Error fetching posts:', error);
      }
    };

    fetchPosts();
  }, []);

  return (
    <div>
      <h2>Posts</h2>
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default PostList;
```
Sada, kreirajmo test za ovu komponentu, mokirajući API zahtjeve:
```javascript
// src/components/PostList.test.js

import React from 'react';
import { render, screen } from '@testing-library/react';
import axios from 'axios';
import PostList from './PostList';

test('renders a list of posts', async () => {
  // Mocking Axios for unit testing
  jest.mock('axios');
  axios.get.mockResolvedValue({ data: [{ id: 1, title: 'Post 1' }, { id: 2, title: 'Post 2' }] });

  // Render the component
  render(<PostList />);

  // Wait for the component to render with fetched data
  const post1Element = await screen.findByText('Post 1');
  const post2Element = screen.getByText('Post 2');

  // Check if the posts are displayed correctly
  expect(post1Element).toBeInTheDocument();
  expect(post2Element).toBeInTheDocument();
});
```
U ovom testu, mokiramo Axios biblioteku kako bismo simulirali uspješan API odgovor koji sadrži niz objava. Test provjerava da li `PostList` komponenta renderuje očekivane objave.

### End-to-End testiranje sa alatima poput Cypress-a
End-to-End (E2E) testiranje osigurava da cijela vaša aplikacija radi besprijekorno, uključujući interakcije između različitih komponenti. Cypress je moćan E2E alat za testiranje web aplikacija, koji pruža jednostavan API za pisanje testova.

Kreirajmo jednostavan Cypress test kako bismo osigurali da naša React aplikacija ispravno interaguje sa RESTful API-jem:

```javascript
// cypress/integration/api_integration_spec.js

describe('API Integration Tests', () => {
  it('successfully fetches user data from the API', () => {
    cy.intercept('GET', 'https://api.example.com/users/1', { fixture: 'user.json' });

    cy.visit('/user-profile/1');

    cy.get('h2').should('contain.text', 'John Doe');
    cy.get('p').should('contain.text', 'Email: john@example.com');
  });

  it('successfully fetches and displays posts from the API', () => {
    cy.intercept('GET', 'https://api.example.com/posts', { fixture: 'posts.json' });

    cy.visit('/post-list');

    cy.get('li').should('have.length', 2);
    cy.get('li').first().should('contain.text', 'Post 1');
    cy.get('li').last().should('contain.text', 'Post 2');
  });
});
```

U ovom Cypress testu, koristimo komandu `cy.intercept` da presretnemo API zahtjeve i odgovorimo sa unaprijed definisanim fajlovima (`user.json` i `posts.json`). Test zatim posjećuje različite rute aplikacije i provjerava da li se prikazuju očekivani podaci.

Da biste pokrenuli Cypress testove, osigurajte da imate instaliran Cypress:
```javascript
npm install cypress --save-dev
```

I dodajte skriptu u vaš `package.json`:

```javascript
"scripts": {
  "cypress:open": "cypress open"
}
```

Pokrenite Cypress koristeći:

```javascript
npm run cypress:open
```

Ovi end-to-end testovi pomažu da se osigura da cijela vaša aplikacija, uključujući interakcije sa RESTful API-jima, funkcioniše ispravno.

## Zaključak
Rad sa RESTful API-jima u Reactu otvara svijet mogućnosti za izgradnju dinamičnih i web aplikacija vođenih podacima. Od dohvaćanja i prikazivanja podataka do rukovanja korisničkim unosom i autentifikacijom, ovaj vodič je obuhvatio širok spektar tema kako bi vam pomogao da postanete vješti u integraciji API-ja sa vašim React projektima.

Zapamtite da ključ uspješne integracije API-ja leži u razumijevanju principa REST-a, odabiru pravih alata i biblioteka, te praćenju najboljih praksi za organizaciju koda, obradu grešaka i sigurnost. Redovno testiranje, kako jedinično tako i end-to-end testiranje, osigurava pouzdanost i robusnost vaše aplikacije.