# Class Instructions

## Get on Class Server

- **Tailscale Invite:** [Click Here](https://login.tailscale.com/admin/invite/H7DGph6CazL)
- **IP Address:** `144.17.92.21` or your tailscales ip alex-server-1
- **Username:** Same as last semester.

## Steps to Follow

1. **Create a Public GitHub Repo:**
   - Go to GitHub and create a new repository.

2. **Initialize Vite Project:**
   - Run the following command in your local machine within the repository:
     ```bash
     npm create vite@latest
     ```
   - Push the Vite project to your GitHub repository.
3. **Setup Docker Files:**
   **Location of files**
  ```plaintext
  
     ├── public/
     ├── src/
     ├── .dockerignore
     ├── .gitignore
     ├── Dockerfile
     ├── README.md
     ├── eslint.config.js
     ├── index.html
     ├── package-lock.json
     ├── package.json
     ├── tsconfig.app.json
     ├── tsconfig.json
     ├── tsconfig.node.json
     └── vite.config.ts
  ```
   - Create a `Dockerfile` in your project directory with the following content(sister to pageke.json file):

     ```Dockerfile
     FROM node:20 as build

     WORKDIR /app
     COPY package*.json ./
     RUN npm install
     COPY . .
     RUN npm run build

     FROM nginx:alpine

     RUN rm -rf /usr/share/nginx/html/*
     COPY --from=build /app/dist /usr/share/nginx/html
     EXPOSE 80
     CMD ["nginx", "-g", "daemon off;"]
     ```
   - Create a `.dockerignore` file with the following content(sister to pageke.json file):
     ```plaintext
     build/
     dist/
     node_modules/
     README.md
     .gitignore
     Dockerfile
     ```
   - Push the Docker-related files to your GitHub repository.

5. **Clone the Repo on Class Machines:**
   - SSH to the `alex` server.
   - Clone your GitHub repository by running:
     ```bash
     git clone https://github.com/MJebran/FrontEnd_deployment.git
     ```
   - Navigate to the project directory:
     ```bash
     cd FrontEnd_deployment/
     ```

6. **Build and Run Docker Container:**
   - Build the Docker image:
     ```bash
     docker build -t mustafa .
     ```
   - Run the Docker container:
     ```bash
     docker run -it --rm -p 0.0.0.0:8288:80 mustafa
     ```

7. **Access Your Project:**
   - Access the project via the following URL: 
     ``` 
     http://144.17.92.21:8288/
     ```

8. **Modify for Your Setup:**
   - Replace `mustafa` with your username.
   - Choose a different port number instead of `8288`.
   - Use the Tailscale IP since you are not on the school network.
