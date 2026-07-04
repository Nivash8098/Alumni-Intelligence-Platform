# AI-Powered Alumni Intelligence Platform
## Comprehensive Setup & Deployment Manual

This manual provides detailed instructions on how to set up, operate, and deploy both the Spring Boot backend and the React frontend of the Alumni Intelligence Platform locally inside VS Code or directly to production.

---

### Project Deliverables Structure

The codebase is split into modular directories designed for rapid deployment:
1. **`/database`**: Contains `mysql_schema.sql` to initialize the database structure and load starting datasets.
2. **`/spring-boot-backend`**: Contains the complete Java files, models, controllers, JPA repositories, token security configuration, and the Maven `pom.xml` configuration.
3. **`/src`**: Configures the high-fidelity responsive React + Tailwind CSS client-side dashboards and visualizations.
4. **`/server.ts`**: Express server acting as the active Node.js server to run the live preview.

---

### Phase 1: Local MySQL Database Installation & Setup

1. **Start MySQL Server**: Ensure your local MySQL server is active (using MySQL Workbench, XAMPP, or command terminal).
2. **Execute Schema SQL**:
   Import and run `/database/mysql_schema.sql` on your MySQL instance.
   - Run via MySQL CLI:
     ```sh
     mysql -u your_username -p < database/mysql_schema.sql
     ```
   - This creates the `alumni_db` schema, builds the `users`, `alumni`, `career_history`, and `mentorship` tables, and loads the active, pre-calibrated sample directory entries automatically.

---

### Phase 2: Backend Spring Boot Setup inside VS Code

1. **Prerequisites**:
   - Ensure **Java Development Kit (JDK 17)** is installed.
   - Install the **Extension Pack for Java** in VS Code.
   - Install the **Spring Boot Extension Pack** in VS Code.

2. **Open Project**:
   - Open VS Code. Load the directory `/spring-boot-backend` inside a new window.
   - Let VS Code import the Maven project (this reads `pom.xml` and downloads external packages like Spring Boot Web, JPA/Hibernate, JJWT, and standard drivers).

3. **Configure Database Properties**:
   - Locate or create `src/main/resources/application.properties` (or `application.yml`):
     ```properties
     spring.datasource.url=jdbc:mysql://localhost:3306/alumni_db?useSSL=false&serverTimezone=UTC
     spring.datasource.username=YOUR_MYSQL_USERNAME
     spring.datasource.password=YOUR_MYSQL_PASSWORD
     spring.jpa.hibernate.ddl-auto=update
     spring.jpa.show-sql=true
     
     # Optional: Enable CORS mapping for the Vite frontend port
     ```

4. **Run Application**:
   - Open `/src/main/java/com/college/alumni/model/Models.java` or click the Spring Boot Dashboard side button in VS Code.
   - Hit **Run** or use terminal:
     ```sh
     mvn spring-boot:run
     ```
   - The server boots by default on port `8080`.

---

### Phase 3: Client React Implementation & Launch

1. **Prerequisites**:
   - Ensure **Node.js (version 18 or higher)** and `npm` are installed.

2. **Open Front-end Workspace**:
   - Load the workspace root in VS Code.
   - Populate local environment configurations:
     Copy `.env.example` as `.env` and fill the variables:
     - `GEMINI_API_KEY`: Supply your Google AI Studio API key.

3. **Install Dependencies & Launch**:
   - Run instructions:
     ```sh
     npm install
     npm run dev
     ```
   - The React client builds instantly using Vite. Access the preview at the printed localhost URL.

---

### Phase 4: Production Deployment

#### Standard Containerised Deployment (e.g., Cloud Run or AWS ECS)
1. Both the backend and compiled frontend files can be packaged into simple Docker containers.
2. The provided `package.json` configurations are set to automatically bundle the Express-wrapped backend alongside compiled React client assets inside `/dist` for easy single-port execution:
   ```sh
   npm run build
   npm start
   ```

---

### Test Account Credentials
To make presentation, review, and grading a seamless 2-second experience, use any of these credentials with the password set to `password`:
- **Undergraduate Alumnus**: `rajesh@college.edu`
- **Department Coordinator**: `cse_dept@college.edu`
- **College Council Admin**: `admin@college.edu`
