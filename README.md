# Activity Answers — Data Visualization

| | |
|---|---|
| **Name** | Saul Ruiz Peña |
| **University** | Universidad Politécnica de Yucatán |
| **Semester** | 4th Quadrimester |
| **Major** | University Technician in Data Science |

---

## WB1.1 — SQL Queries with Python

### Section 1 — Data Access with Queries

**1. Create a connection and cursor to the database.**

A connection to `music.db` was established using `sqlite3.connect()`, and a cursor was created using `connection.cursor()`. The cursor allows executing SQL queries against the database.

**2. Explore all columns in all the previously mentioned tables. Show the first 10 records.**

- `songs`: Columns are `_id`, `track`, `title`, `album`. First 10 records retrieved with `SELECT * FROM songs LIMIT 10`.
- `albums`: Columns are `_id`, `name`, `artist`. First 10 records retrieved with `SELECT * FROM albums LIMIT 10`.
- `artists`: Columns are `_id`, `name`. First 10 records retrieved with `SELECT * FROM artists LIMIT 10`.

**3. Iron Maiden has `_id = 8` in the artists table. Use this id to identify their albums in the `albums` table.**

Using `WHERE artist = 8`, the following albums were found:

| _id | Name | Artist |
|-----|------|--------|
| 236 | The Number of the Beast | 8 |
| 412 | Powerslave | 8 |
| 420 | Seventh Son Of A Seventh Son | 8 |

**4. Show the songs from the album "The Number of the Beast" in alphabetical order.**

| Title |
|-------|
| 22 Acacia Avenue (1998 Digital Remaster) |
| Children Of The Damned (1998 Digital Remaster) |
| Gangland (1998 Digital Remaster) |
| Hallowed Be Thy Name (1998 Digital Remaster) |
| Invaders (1998 Digital Remaster) |
| Run To The Hills (1998 Digital Remaster) |
| The Number Of The Beast (1998 Digital Remaster) |
| The Prisoner (1998 Digital Remaster) |
| Total Eclipse (1998 Digital Remaster) |

---

### Section 2 — Data Aggregations and Groupings

**1. How many songs, albums, and artists are registered in the database?**

| Table | Count |
|-------|-------|
| Songs | 5,350 |
| Albums | 439 |
| Artists | 201 |

**2. Group the `albums` table by artist to identify the 5 artists with the most albums.**

| Artist ID | Number of Albums |
|-----------|-----------------|
| 36 | 18 |
| 16 | 15 |
| 64 | 14 |
| 196 | 13 |
| 152 | 13 |

**3. Present the names of the artists identified in the previous point.**

| Artist Name | Number of Albums |
|-------------|-----------------|
| Black Sabbath | 18 |
| Axel Rudi Pell | 15 |
| Led Zeppelin | 14 |
| Deep Purple | 13 |
| Aerosmith | 13 |

**4. Which album has the most songs?**

The album with the most songs is **"Cornology"** by **Bonzo Dog Band**, with **72 songs**. *Cornology* is a three-volume compilation box set released in 1992, collecting the complete recorded output of the British comedy rock band Bonzo Dog Doo-Dah Band.

---

### Section 3 — Combining Tables

**1. Show all song names from the album "Seventh Son Of A Seventh Son" (`_id = 420`) in track order.**

| Track | Title |
|-------|-------|
| 1 | Moonchild (1998 Digital Remaster) |
| 2 | Infinite Dreams (1998 Digital Remaster) |
| 3 | Can I Play With Madness (1998 Digital Remaster) |
| 4 | The Evil That Men Do (1998 Digital Remaster) |
| 5 | Seventh Son Of A Seventh Son (1998 Digital Remaster) |
| 6 | The Prophecy (1998 Digital Remaster) |
| 7 | The Clairvoyant (1998 Digital Remaster) |
| 8 | Only The Good Die Young (1998 Digital Remaster) |

**2. Get all songs by Aerosmith in alphabetical order. Only include the title. How many are there?**

Aerosmith has **151 songs** registered in the database, retrieved using a JOIN across the `songs`, `albums`, and `artists` tables filtered by `ar.name = 'Aerosmith'`, ordered alphabetically.

---

## WB1.2 — JSON Usage (Place Details API — Google Maps)

**1. Which of the following URLs was used to obtain the provided file?**

**Answer: c.**
`https://maps.googleapis.com/maps/api/place/details/json?place_id=ChIJ84KkeFxxVo8ReWeMn3zwrfI&key=1a2b3c4d5e6f7g`

The output format is `json` (not `xml`), and multiple parameters are separated by `&` (not `,`).

**2. What is the price level of the place?**

**Answer: b — 2**

The `price_level` field in the JSON returns `2`, indicating a moderately priced establishment on a scale of 0 to 4.

**3. What is the average rating of the place?**

**Answer: b — 4.5**

The `rating` field returns `4.5`, based on a total of 5,824 user ratings.

**4. Which of the following types is NOT included in the description of the place?**

**Answer: d — restaurant**

The `types` field contains: `["food", "point_of_interest", "store", "establishment"]`. The type `restaurant` is not present.

**5. How many reviews were retrieved as part of the place details?**

**Answer: b — 5**

The `reviews` array contains exactly 5 entries.

**6. In what language are most reviews written?**

**Answer: b — English**

All 5 reviews have `"language": "en"` (English).

**7. What is the lowest rating given in the reviews?**

**Answer: b — 3**

The review ratings are `[3, 5, 3, 5, 4]`. The minimum rating is **3**, given by Leonard Majere and S H.

**8. Which of the following flavors is mentioned in the comments?**

**Answer: d — Coco (Coconut)**

Reviewer S H writes: *"I had the famous Helado de Coco."* No mentions of strawberry, vanilla, or chocolate were found.

---

## WB1.2B — DENUE API

**1. Create a `BuscarEntidad()` function in Python that receives the input parameters, queries the API, and returns a DataFrame with the results.**

A function named `BuscarEntidad()` was implemented with the parameters `condicion`, `entidad`, `registro_inicial`, `registro_final`, and `token`. It builds the request URL following the DENUE API format, performs a GET request using the `requests` library, parses the JSON response, and returns the result as a `pandas` DataFrame.

**2. Considering `data_dataframe`, what are the `Clase_actividad` with the most records?**

After querying all establishments in Chiapas (entity 7) using `condicion = 'todos'`, the `Clase_actividad` column was grouped with `value_counts()`. The activity classes with the highest number of registered establishments correspond to retail commerce and food services sectors, which are the most common economic activities in the state.

**3. Considering `data_dataframe`, what are the `Estrato` with the most records?**

The `Estrato` column (which represents the number of employees) was grouped with `value_counts()`. The stratum with the most records is **"0 a 5 personas"** (0 to 5 employees), which reflects that the vast majority of economic units in Chiapas are micro-businesses.

**4. Read about the `Buscar` method. Create a function in Python and locate establishments within 100 m of the Parque Central de Tuxtla Gutiérrez.**

A function named `Buscar()` was implemented with parameters `palabras`, `latitud`, `longitud`, `distancia`, `registro`, and `token`. It queries the DENUE `Buscar` endpoint using the coordinates of the Parque Central de Tuxtla Gutiérrez (latitude: 16.7530, longitude: -93.1130) with a radius of 100 meters.

**5. What are the `Clase_actividad` with the most records in the previous query?**

From the establishments located within 100 meters of the Parque Central de Tuxtla Gutiérrez, the predominant activity classes correspond to food and beverage services (restaurants, cafés, street food stands) and retail commerce — consistent with the commercial and touristic character of the city center area.
