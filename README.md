# Customer Management API

This is an API for managing customer data. It provides CRUD (Create, Read, Update, Delete) operations for customer records.

## Technologies Used

*   Node.js
*   Fastify
*   Prisma
*   MongoDB

## Features

*   Create new customers
*   List existing customers
*   Delete customers

## Prerequisites

*   Node.js (v16 or higher)
*   npm (or yarn)
*   MongoDB

## Setup and Configuration

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd backend
    ```

2.  **Install dependencies:**

    ```bash
    npm install
    ```

3.  **Configure the Database:**

    *   This application uses MongoDB as its database. You need to have a MongoDB instance running. You can either:
        *   Install MongoDB locally.
        *   Use a cloud-based MongoDB service like MongoDB Atlas.

    *   Create a database.

4.  **Configure the `.env` file:**

    *   Create a `.env` file in the root directory of the project.
    *   Add the following environment variable, replacing `<your_mongodb_connection_string>` with your actual MongoDB connection string:

        ```
        DATABASE_URL=<your_mongodb_connection_string>
        ```

        ```
        DATABASE_URL=mongodb+srv://<username>:<password>@<cluster_url>/databasename?retryWrites=true&w=majority
        ```

        **Important:** Ensure your MongoDB server is running as a replica set. See [https://pris.ly/d/mongodb-replica-set](https://pris.ly/d/mongodb-replica-set) for instructions.

5.  **Generate Prisma Client:**

    ```bash
    npx prisma generate
    ```

    This command generates the Prisma client based on your `schema.prisma` file and the `DATABASE_URL` in your `.env` file.

## Running the Application

1.  **Start the development server:**

    ```bash
    npm run dev
    ```

    (Note: You'll need to define a `start` script in your `package.json` that executes `node src/server.ts` or similar.  The provided `package.json` is missing this.)

2.  **Access the API:**

    The API will be running at `http://localhost:3333`.

## API Endpoints

*   `POST /customer`: Create a new customer.  Requires `name` and `email` in the request body.
*   `GET /customers`: List all customers.
*   `DELETE /customer`: Delete a customer.  (Currently, this endpoint doesn't specify *which* customer to delete.  You'll need to modify `DeleteCustomerController.ts` and `routes.ts` to accept an ID.)

## Important Considerations

*   **Error Handling:** The application includes basic error handling, but you may want to enhance it for production use.
*   **Validation:** Input validation is minimal. You should add more robust validation to prevent invalid data from being stored in the database.
*   **Security:** This is a basic example and does not include any security measures. You should implement appropriate security measures (e.g., authentication, authorization) before deploying this application to a production environment.
*   **Missing `start` script:** The provided `package.json` file does not include a `start` script. You will need to add one to run the application using `npm start`.  A basic example would be:

    ```json
    "scripts": {
      "start": "node dist/server.js",
      "dev": "ts-node-dev src/server.ts",
      "build": "tsc",
      "generate": "prisma generate"
    }
    ```

    You'll also need to build the project first using `npm run build` if you use the `start` script above.  The `dev` script requires `ts-node-dev` to be installed (`npm install -D ts-node-dev`).
```

