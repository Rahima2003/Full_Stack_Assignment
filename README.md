**Pokemon App**

This is a full-stack application for managing Pokemon using a React frontend and an Express.js backend. The application allows users to add, edit, and delete Pokemon details.

**Project Structure**

pokemon-app/

│

├── client/

│   ├── public/

│   │   └── index.html

│   ├── src/

│   │   ├── components/

│   │   │   ├── AddPokemonUser.js

│   │   │   ├── ListPokemonUsers.js

│   │   │   └── AddPokemon.js

│   │   ├── App.js

│   │   └── index.js

│   ├── package.json

│   └── README.md

│

├── server/

│   ├── data.json

│   ├── index.js

│   ├── package.json

│   └── README.md

│

└── README.md


**Client**

The client directory contains the React application. It includes:

**public/:** Public assets and the index.html file.

**src/:** React components, styles, and other frontend code.

**package.json:** Dependencies and scripts for the React application.

**Server**

The server directory contains the Express.js server. It includes:

**index.js:** The main server file with API endpoints.

**data.json:** A JSON file to store user data.

**package.json:** Dependencies and scripts for the server.


**Express Server Setup:**

Imports necessary modules: express, body-parser, cors, fs, node-fetch.

Initializes the Express app and sets up middleware for JSON parsing and CORS.

Reads initial data from data.json.

**API Endpoints:**

GET /api/pokemon: Fetches a list of Pokemon from the PokeAPI.

GET /api/pokemon/:name/abilities: Fetches abilities for a specific Pokemon from the PokeAPI.

CRUD operations for user data: Handles fetching, adding, updating, and deleting user data.






