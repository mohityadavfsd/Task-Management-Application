# Task Management Application

A full-stack task management web app built with:

- Frontend: HTML, CSS, JavaScript
- Backend: Node.js + Express
- Database: MongoDB + Mongoose

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a `.env` file from `.env.example` and update the MongoDB connection string:

   ```bash
   cp .env.example .env
   ```

3. Start the app:

   ```bash
   npm run dev
   ```

4. Open `http://localhost:4000`

## API Endpoints

- `GET /api/tasks`
- `POST /api/tasks`
- `PUT /api/tasks/:id`
- `DELETE /api/tasks/:id`

## Deployment

This project is a full-stack Node.js application. The frontend and backend are deployed together, with Express serving the app and API.

### Azure App Service Deployment

1. Create a MongoDB database using Azure Cosmos DB with MongoDB API or MongoDB Atlas.
2. Create an Azure Web App for Node.js.
3. Add these App Settings in Azure Web App configuration:
   - `MONGO_URI` = your MongoDB connection string
   - `JWT_SECRET` = a strong secret value
   - `PORT` = `4000`
4. Add a GitHub secret named `AZURE_WEBAPP_PUBLISH_PROFILE` with the publish profile XML from Azure.
5. Add a GitHub secret named `AZURE_WEBAPP_NAME` with your Web App name.
6. Push to `main`; the workflow at `.github/workflows/azure-webapp-deploy.yml` will deploy the app.
### Azure CLI Deployment

Use the following CLI flow to create the App Service and deploy from the repository root:

```bash
export AZURE_WEBAPP_NAME="your-app-name"
export AZURE_RESOURCE_GROUP="your-resource-group"
export AZURE_LOCATION="eastus"
export MONGO_URI="your-mongo-uri"
export JWT_SECRET="your-jwt-secret"

bash azure-deploy.sh
```

If you are on Windows PowerShell, set the variables like this:

```powershell
$env:AZURE_WEBAPP_NAME = "your-app-name"
$env:AZURE_RESOURCE_GROUP = "your-resource-group"
$env:AZURE_LOCATION = "eastus"
$env:MONGO_URI = "your-mongo-uri"
$env:JWT_SECRET = "your-jwt-secret"
bash azure-deploy.sh
```

### MongoDB Atlas Setup

1. Sign in to MongoDB Atlas and create a new project.
2. Build a free cluster and add a database user with a strong password.
3. Allow your app IP address or allow access from anywhere for testing.
4. Copy the connection string from Atlas and replace the placeholders:

```text
mongodb+srv://<username>:<password>@<cluster-url>/task_management?retryWrites=true&w=majority
```

5. Use that URI for `MONGO_URI` in Azure App Settings or your local environment.

### PowerShell Azure Deployment

On Windows, use the included PowerShell helper:

```powershell
$env:AZURE_WEBAPP_NAME = "your-app-name"
$env:AZURE_RESOURCE_GROUP = "your-resource-group"
$env:AZURE_LOCATION = "eastus"
$env:MONGO_URI = "your-mongo-uri"
$env:JWT_SECRET = "your-jwt-secret"

./azure-deploy.ps1
```

### Local Docker Deployment

Build and run locally using Docker:

```bash
docker build -t task-management-app .
docker run -d -p 4000:4000 --name task-app \
  -e MONGO_URI="your-mongo-uri" \
  -e JWT_SECRET="your-jwt-secret" \
  task-management-app
```
