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

**Backend Explanation**

This backend is implemented using Node.js with the Express framework. It provides a RESTful API for managing Pokemon data and user data. 

**Importing Required Modules**

import express from 'express';

import bodyParser from 'body-parser';

import cors from 'cors';

import fs from 'fs';

import fetch from 'node-fetch';

**express:** A minimal and flexible Node.js web application framework.

**bodyParser:** Middleware to parse incoming request bodies in a middleware before your handlers, available under the req.body property.

**cors:** Middleware to enable Cross-Origin Resource Sharing.

**fs:** Module to interact with the file system.

**node-fetch:** A light-weight module that brings window.fetch to Node.js.

-**Setting Up the Express Application**

const app = express();

app.use(bodyParser.json());

app.use(cors());

**app:** Initializes the Express application.

**app.use(bodyParser.json()):** Configures the app to use body-parser for parsing JSON request bodies.

**app.use(cors()):** Configures the app to use CORS, allowing cross-origin requests.

**Loading Data from JSON File**

let data = JSON.parse(fs.readFileSync('data.json', 'utf-8'));

**data:** Loads user data from data.json and parses it into a JavaScript object.

**Pokemon API URL**

const POKE_API_URL = 'https://pokeapi.co/api/v2/pokemon-species/';

**POKE_API_URL:** Base URL for fetching Pokemon data from the PokeAPI.

**Fetch a List of Pokemon**

app.get('/api/pokemon', async (req, res) => {

    try {
    
        const response = await fetch(`${POKE_API_URL}?limit=151`);
        
        const data = await response.json();
        
        res.json(data.results);
        
    } catch (error) {
    
        res.status(500).json({ error: 'Failed to fetch Pokemon data' });
        
    }
    
    });

Endpoint: /api/pokemon

Method: GET

Description: Fetches a list of 151 Pokemon from the PokeAPI.

Error Handling: Returns a 500 status code if the request fails.

**Fetch Abilities for a Specific Pokemon**

app.get('/api/pokemon/:name/abilities', async (req, res) => {

    const { name } = req.params;
    
    try {
    
        const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${name}`);
        
        const data = await response.json();
        
        res.json(data);
        
    } catch (error) {
    
        res.status(500).json({ error: 'Failed to fetch Pokemon abilities' });
        
    }
    
    });

Endpoint: /api/pokemon/:name/abilities

Method: GET

Description: Fetches abilities for a specific Pokemon by name from the PokeAPI.

Error Handling: Returns a 500 status code if the request fails.


**CRUD Operations for User Data**

**Get All Users**

app.get('/api/users', (req, res) => {

    res.json(data);
    
});

Endpoint: /api/users

Method: GET

Description: Returns all user data.


**Add or Update a User**

app.post('/api/users', (req, res) => {

    const newUser = req.body;
    
    const existingUserIndex = data.findIndex(user => user.ownerName === newUser.ownerName);
    
    if (existingUserIndex !== -1) {
    
        data[existingUserIndex] = newUser;  // Update existing user
        
    } else {
    
        data.push(newUser);  // Add new user
        
    }
    
    fs.writeFileSync('data.json', JSON.stringify(data));
    
    res.status(201).json(newUser);
    
});

Endpoint: /api/users

Method: POST

Description: Adds a new user or updates an existing user.

Body: JSON object representing the user.

Success: Returns the added or updated user.

Error Handling: Returns a 201 status code upon successful creation or update.

**Update an Existing User**

app.put('/api/users/:ownerName', (req, res) => {

    const { ownerName } = req.params;
    
    const updatedUser = req.body;
    
    const userIndex = data.findIndex(user => user.ownerName === ownerName);
    
    if (userIndex !== -1) {
    
        data[userIndex] = updatedUser;
        
        fs.writeFileSync('data.json', JSON.stringify(data));
        
        res.json(updatedUser);
        
    } else {
    
        res.status(404).json({ error: 'User not found' });
        
    }
    
    });

Endpoint: /api/users/:ownerName

Method: PUT

Description: Updates an existing user.

Params: ownerName - the name of the user to update.

Body: JSON object representing the updated user.

Success: Returns the updated user.

Error Handling: Returns a 404 status code if the user is not found.

**Delete a User**

app.delete('/api/users/:ownerName', (req, res) => {

    const { ownerName } = req.params;
    
    data = data.filter(user => user.ownerName !== ownerName);
    
    fs.writeFileSync('data.json', JSON.stringify(data));
    
    res.status(204).end();
    
    });

Endpoint: /api/users/:ownerName

Method: DELETE

Description: Deletes a user.

Params: ownerName - the name of the user to delete.

Success: Returns a 204 status code upon successful deletion.

**Starting the Server**

const PORT = 5000;

app.listen(PORT, () => {

    console.log(`Server is running on port ${PORT}`);
    
});

Starts the Express server on port 5000.



**Express Server Setup:**

Imports necessary modules: express, body-parser, cors, fs, node-fetch.

Initializes the Express app and sets up middleware for JSON parsing and CORS.

Reads initial data from data.json.

**API Endpoints:**

GET /api/pokemon: Fetches a list of Pokemon from the PokeAPI.

GET /api/pokemon/:name/abilities: Fetches abilities for a specific Pokemon from the PokeAPI.

CRUD operations for user data: Handles fetching, adding, updating, and deleting user data.






