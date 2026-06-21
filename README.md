# :musical_note: SPOTIFY BROWSER

## :open_book: OVERVIEW
Date: February 2025\
Developer(s): Ashneet Rathore

Spotify Browser is a full-stack web application for searching and browsing Spotify content by artist, track, and album categories. The app uses the Spotify Web API to retrieve real-time music data, presented through an intuitive, component-driven browsing interface. Users can seamlessly navigate between related results, such as exploring an artist's albums or viewing the tracks within an album. 

**Tech Stack** | Node.js, Express, Spotify Web API, Angular, TypeScript, HTML, CSS, Bootstrap

## :film_strip: DEMO
[Watch the demo on Youtube](https://youtu.be/Iu-WppmJ8cI)

## :classical_building: ARCHITECTURE
The backend is implemented in **Node.js** with an **Express** webserver, and the frontend is built with **Angular (TypeScript)**, **HTML**, **CSS**, and **Bootstrap**. The backend also manages **OAuth 2.0 authentication**, storing tokens to make authorized API requests without exposing credentials to the frontend.

The following illustrates the flow of a search request:

- Angular captures the search input and sends an HTTP request to an Express endpoint
- Express receives the request, makes a corresponding call to the **Spotify Web API**, and returns JSON data to Angular
- Angular processes the returned data into structured TypeScript objects
- Page components render the objects using UI widgets - carousels for artists and albums, tables for tracks

## :page_facing_up: PAGES AND FEATURES
Description of the pages in the application:
- Home Page | Displays information about the logged-in user's account and contains the main search feature, which supports keyword-based searching by artist, album, or track
- Artist Page | Shows artist details, including profile picture, popularity stats, a carousel of their albums and a table of their top tracks
- Album Page | Shows album details, including album cover, popularity, associated artist, and track list
- Track Page | Displays track details, including duration, popularity, and associated artist and album

## :open_file_folder: PROJECT FILE STRUCTURE
> [!NOTE]
> The overview of the file structure is intentionally kept minimal. Additional directories/files exist in the project.
```bash
spotify-browser/
│── client/                             # Angular client
│   └── src/
│       └── app/
│           │── components/             # Reusable UI widgets (caraousels, tables)
│           │── data/                   # Typescript classes for API response data
│           │── pages/                  # Page components
│           │── services/               # HTTP request logic for Express endpoints
│           └── app-routing.module.ts   # URL route to page mappings
│── webserver/                          # Express/Node.js backend
│   └── routes/
│       └── index.js                    # Backend API routes and Spotify API communication
│── README.md                           # Project documentation
└── .gitignore                          # Ignored files
```

## :hammer: CONFIGURATION
### :headphones: SPOTIFY APP SETUP
1. Create or log into a Spotify Developer account at [https://developer.spotify.com/](https://developer.spotify.com/)
2. On the [Dashboard](https://developer.spotify.com/dashboard), click `Create app`.
3. Enter an app name and description.
4. In the *Redirect URIs* field, enter in *http://127.0.0.1:8888/callback* and click `Add`.
5. Under *Which API/SDKs are you planning to use?*, select `Web API`.
6. Check *Developer Terms of Service* and click `Save`. A *Client ID* and *Client Secret* will be generated under the *Basic Information* tab.

### :computer: ENVIRONMENT SETUP
**1. Clone the repository**
```bash
git clone https://github.com/ashneetrathore/spotify-browser.git
```

**2. Create two configuration files in `webserver/`**

`client_secret.json` will store the Spotify API credentials generated earlier. Replace the placeholder values with the actual credentials and use the following format:
```json
{
  "client_id": "INSERT CLIENT KEY HERE",
  "client_secret": "INSERT CLIENT SECRET HERE"
} 
```

`tokens.json` will store access and refresh tokens needed for authentication. It will be automatically updated once the tokens are retrieved, so use the following format:
```json
{
  "access_token": null,
  "refresh_token": null
 }
```

**3. Install dependencies in `webserver/`**
```bash
cd spotify-browser/webserver
npm install
```

**4. Install dependencies in `client/`**
```bash
cd spotify-browser/client
npm install
```

## :rocket: EXECUTION
Start the webserver (in `webserver/`)
```bash
npm start
```

Run the Angular client in a separate terminal (in`client/`)
```bash
ng serve --open
```

The app will automatically open at [http://localhost:4200/](http://localhost:4200/).

## :wrench: TRY IT OUT
### :key: LOGIN AS SPOTIFY USER
1. In the top navigation bar, click `Log in`.
2. Log in with the Spotify account used to create the Spotify Developer app and authorize access.
4. Click `Load info about me` to display profile information, including username, profile picture, and a link to the Spotify profile.

> [!NOTE]
> Steps 2 and 3 are only required for the first log in. On subsequent visits, clicking `Log in` will automatically use stored credentials.

### :mag: PERFORM SEARCHES
Type a keyword (e.g. artist name, album title, track title), select a search type from the dropdown (*artist*, *album*, or *track*), and click `Search`.

**1. Artist Search**\
Results are displayed in a carousel. Use the ⟩ button to browse and click a result to navigate to the Artist page.

**2. Album Search**\
Results are displayed in a carousel. Use the ⟩ button to browse and click a result to navigate to the Album page.

**3. Track Search**\
Results are displayed in a table, where each track links to its associated Track, Artist, and Album pages.