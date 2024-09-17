
# Make Your Burger

**Make Your Burger** is a Single Page Application (SPA) developed with Vue.js. It allows users to easily and intuitively build their own burgers. The application also provides an interface for the production team, facilitating order management.

## Features

- **Burger Assembly:** Interactive interface for selecting ingredients and customizing burgers.
- **Simulated Backend:** Uses *json-server* to simulate order storage.
- **Order Management:** Interface for the production team to update order statuses from "in progress" to "completed."

## Technologies Used

- **Vue.js 3.2.13:** Main framework for building the interface.
- **Vue Router 4.0.3:** Route management for smooth navigation within the SPA.
- **json-server 1.0.0-beta.1:** Simulates a backend for data storage.
- **core-js 3.8.3:** Compatibility library for older browsers.

## Installation

1. **Clone the Repository**

   git clone https://github.com/your-username/makeyourburger.git
   cd makeyourburger

   
2. **Install Dependencies**
   npm install

3. **Start the Development Server**
   npm run serve

4. **Start the Simulated Backend**
   In a separate terminal, start the json-server to simulate the backend:

    npm run server
    The command npm run server should be configured in your package.json to run json-server --watch db/db.json.

Usage
Access the application in your browser at http://localhost:8080.
Build your burger by selecting ingredients.
View and manage orders using the production interface.
Contributing
If you want to contribute to the project, please follow these steps:

Fork the repository.
Create a new branch for your changes (git checkout -b my-new-feature).
Make your changes and stage them (git add .).
Commit your changes (git commit -m "Add new feature").
Push the branch to the remote repository (git push origin my-new-feature).
Open a pull request on GitHub.
License
This project is licensed under the MIT License.

Feel free to adjust as needed and add more specific details about your project!
