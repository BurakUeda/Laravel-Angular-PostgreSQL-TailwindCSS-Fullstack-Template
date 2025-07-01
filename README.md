# Laravel 12 and Angular Fullstack Template
This is a complete, Docker-based fullstack development environment including:
- <img height="14" src="img.png" width="14" alt=""/> Laravel/PHP API backend
- ⚙️ Angular frontend with TailwindCSS v4
- 🐘 PostgreSQL
- 🌐 Nginx (for serving production builds)

You don't need Node.js and Composer installed on your computer.

## Requirements
[Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running.

---

## 🛠️ Installation

### 1) Set Up Your App Name and Database Credentials
Create a `.env` file in the project root:
```dotenv
APP_NAME=my_app
DB_NAME=app_db
DB_USER=app_user
DB_PASSWORD=supersecurepassword
```

---
### 2) Creating Laravel Backend
1. Open a terminal in your project’s root folder.
2. Run the following command to generate your Laravel app inside the `backend` folder.
```bash
docker run --rm -v "${PWD}/backend:/app" -w /app laravelsail/php83-composer:latest bash -c "composer create-project laravel/laravel ."
```

---
### 3) Create the Angular Frontend
1. Open a terminal in your project’s root folder.
2. Run the following command to generate your Angular app inside the `frontend` folder.
```bash
docker run -it --rm -v "${PWD}/frontend:/app" -w /app node:22 sh -c "npm install -g @angular/cli && ng new YOUR-APP-NAME-HERE --directory=. --style=css --routing --strict --skip-git --skip-install --force"
```
>🔧 Replace  `YOUR-APP-NAME-HERE` with your project name.
3. To enable hot reload (instant updates on file change), edit `frontend/package.json`.

Change:
```json
"start": "ng serve"
```
To:
```json
"start": "ng serve --host 0.0.0.0 --port 4200 --poll=1000"
```
---
### 4) Build and Start All Services
Open a terminal in your project’s root folder and run:
```bash
docker-compose up --build -d
```
>🕐 This may take a minute.
---
### 5) Add TailwindCSS to Angular
1. Inside the `/frontend` folder, run:
```bash
docker-compose exec angular_frontend npm install tailwindcss @tailwindcss/postcss postcss --force
```
2. Create a `frontend/.postcssrc.json` file:
```json
{
  "plugins": {
    "@tailwindcss/postcss": {}
  }
}
```
3. Edit `frontend/src/styles.css` and add:
```css
@import "tailwindcss";
```
### Once everything is done:
- Open http://localhost:4200 to view the Angular app.
- Use `docker ps` to check that all containers are running.
