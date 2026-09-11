# SE Lab - Solved Question Papers (Srija first, then CSE papers)

> Format: each question appears first, with its solution directly below it.
> Ordering: **Part A - Srija's papers** come first (your likely mentor), followed by **Part B - the CSE papers** for coverage.
> Theory answers are written to a length appropriate to their marks.
> Answers are based on the college materials (`Git  GitHUB.pdf`, `Git with Local Repository.docx`, `Git with Remote repository.docx`, `Docker file, Single containerization.docx`, `Maven Java and Web Projects.docx`) and standard Maven/Git/Docker usage.

---

# Part A - Srija's Papers (primary mentor)

## A1. SET-5 - Blood Bank Management System (CSE)

> **Section:** CSE - **Faculty:** S. Srija - **Paper:** SET-5 (Blood Bank)

### Part I - Git & GitHub Collaboration (40)

**Q1) Set up this codebase on your local machine. [2]**

**Answer:** `git clone https://github.com/sarasrija/Blood-Bank-Management-system.git` - creates a local copy; `cd` into the folder to work on it.

**Q2) Verify the remote server connections configured for fetching and pushing code in your project workspace. [2]**

**Answer:** `git remote -v` - lists the remote name (`origin`) with both the fetch and push URLs.

**Q3) You modified src/main/webapp/index.jsp and created src/main/webapp/inventory.jsp. Inspect the current status of all staged, unstaged, and untracked changes. [2]**

**Answer:** `git status` - shows `index.jsp` as modified (unstaged) and `inventory.jsp` as an untracked new file.

**Q4) Move your workspace directly into a new working context named feature/donor-registration using a single operation. [2]**

**Answer:** `git checkout -b feature/donor-registration` - creates and switches to the branch in one command.

**Q5) Determine all local and remote branches in the repository while confirming which branch you are actively on. [2]**

**Answer:** `git branch -a` - lists local and remote branches; the current branch is marked with `*`.

**Q6) You added DonorServlet.java. Save this specific file to the repository history with the log note "Add donor registration servlet". [2]**

**Answer:** `git add src/main/java/com/bloodbank/servlet/DonorServlet.java` then `git commit -m "Add donor registration servlet"`.

**Q7) You realized src/main/webapp/WEB-INF/web.xml was left out of your latest snapshot. Merge this file into that last snapshot without altering the original message. [2]**

**Answer:** `git add src/main/webapp/WEB-INF/web.xml` then `git commit --amend --no-edit` - adds the file to the last commit while keeping its message.

**Q8) A teammate updated pom.xml on GitHub. Retrieve these remote updates without modifying your local working files. [2]**

**Answer:** `git fetch origin` - downloads remote commits to `origin/main` but leaves your working files untouched.

**Q9) Incorporate the latest updates from the remote main branch into your currently active branch. [2]**

**Answer:** `git pull origin main` (or after `git fetch`, `git merge origin/main`) - merges the latest remote main into your branch.

**Q10) Reorder your local feature branch history so that it stems from the tip of the updated main branch. [2]**

**Answer:** `git fetch origin` then `git rebase origin/main` - replays your commits on top of the latest main for a linear history.

**Q11) Conflicts break your rebase process. Cancel the rebase entirely and return your repository to its state prior to the rebase attempt. [2]**

**Answer:** `git rebase --abort` - stops the rebase and restores the branch to where it was before.

**Q12) A faulty test assertion was committed in DonorTest.java. Safely undo the impact of that commit while preserving the commit log history. [2]**

**Answer:** `git revert <commit-hash>` - creates a new commit that reverses the faulty change; history is preserved.

**Q13) Undo your last commit execution while ensuring all modified changes remain staged in index memory. [2]**

**Answer:** `git reset --soft HEAD~1` - undoes the commit but keeps all changes staged.

**Q14) You accidentally committed src/main/resources/db-config.env. Remove this file from project version control while keeping the file saved on your local drive. [2]**

**Answer:** `git rm --cached src/main/resources/db-config.env` -> `git commit -m "Remove db-config.env from tracking"` -> add `db-config.env` to `.gitignore` so it is not tracked again.

**Q15) You must switch branches immediately to handle an emergency, but your changes in inventory.jsp are unfinished. Safely store your uncommitted changes without creating a commit record. [2]**

**Answer:** `git stash` - saves the changes and cleans the working directory, letting you switch branches.

**Q16) View all stored work snapshots and restore your saved inventory.jsp modifications back to your workspace. [2]**

**Answer:** `git stash list` (view) then `git stash apply` (restore, keeping the stash) or `git stash pop` (restore and remove it).

**Q17) Inspect the line-by-line differences between feature/donor-registration and main specifically for src/main/webapp/index.jsp. [2]**

**Answer:** `git diff main feature/donor-registration -- src/main/webapp/index.jsp` - restricts the diff to that file between the two branches.

**Q18) Produce a compact, single-line visual timeline mapping out how project branches have diverged and merged over time. [2]**

**Answer:** `git log --oneline --graph --all` - an ASCII graph with one line per commit showing branches and merges.

**Q19) Work on feature/donor-registration is complete. Return to main and bring the feature branch changes into main. [2]**

**Answer:** `git checkout main` then `git merge feature/donor-registration`.

**Q20) Upload your updated main branch to GitHub, and verify that your local workspace and the remote repository share the exact same commit point. [2]**

**Answer:** `git push origin main`; verify with `git status` ("up to date with 'origin/main'") or by comparing `git log -1 --oneline` with `git log origin/main -1 --oneline`.

### Part II - Maven Java Application Development (40)

### Q1. POM Validation & Plugin Debugging (6)

**Q1a) Running mvn validate on the provided pom.xml results in an immediate build failure during project model parsing. Identify the XML schema violation causing this failure, explain why Maven rejects it, and write the corrected <dependency> configuration. (3)**

**Answer:**
- The POM contains an **invalid element or typo** - the classic example is `<artificatId>` instead of `<artifactId>`, or an unknown tag/attribute.
- Maven's model builder **validates the POM against the Maven XML schema**; any element not in the schema causes an immediate model-parse failure, before any compilation.
- Corrected dependency block (exact element names, in order):
  ```xml
  <dependency>
    <groupId>com.example</groupId>
    <artifactId>library-name</artifactId>
    <version>1.0</version>
  </dependency>
  ```

**Q1b) A developer attempts to run mvn tomcat7:run, but Maven fails to execute the goal. Identify why Maven cannot locate and execute this plugin, and provide the complete, corrected <plugin> block. (3)**

**Answer:**
- The plugin declaration is **missing the `<groupId>`**, so Maven cannot resolve which plugin `tomcat7-maven-plugin` belongs to.
- A plugin is identified by **groupId + artifactId + version**; without all three, the plugin is not found and the goal cannot run.
- Corrected block:
  ```xml
  <plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
  </plugin>
  ```

### Q2. Dependency Resolution & Lifecycle Failures (6)

**Q2a) Executing mvn compile fails because Maven cannot resolve the declared database driver dependency. Identify why artifact resolution fails and write the corrected <dependency> block required for MySQL connectivity. (3)**

**Answer:**
- Resolution fails because the **coordinates are incorrect** (wrong `groupId`, `artifactId`, or `version`, or a version that does not exist in the repository).
- Maven looks the artifact up by `groupId:artifactId:version`; a mismatch means it is never found.
- Corrected MySQL Connector/J block:
  ```xml
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
  </dependency>
  ```

**Q2b) Executing mvn test-compile fails due to an incomplete dependency declaration in the <dependencies> section. Identify the missing element preventing test compilation and provide the corrected <dependency> block. (3)**

**Answer:**
- The declaration is missing the **`<version>`** element - Maven cannot resolve an artifact without a version.
- Corrected block (example, JUnit 5):
  ```xml
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.0</version>
    <scope>test</scope>
  </dependency>
  ```

### Q3. Build Output Analysis (5)

**Q3a) When mvn clean package is executed successfully, what will be the exact name of the generated web archive file inside the target/ directory? Explain the rule governing this output filename. (3)**

**Answer:**
- The name is **`<finalName>.war`** if a `<finalName>` is configured, otherwise the default **`artifactId-<version>.war`** (e.g. `bloodbank-0.0.1-SNAPSHOT.war`).
- **Rule:** Maven names the artifact using the `<finalName>` element if present; otherwise it uses `artifactId-version` and appends the packaging extension (`.jar` or `.war`).
- This name also becomes the **context path** when deployed to Tomcat (e.g. `/bloodbank/`).

**Q3b) Based on the embedded web server plugin configuration, what context path URL would normally be used to access the application upon local server execution? (2)**

**Answer:** `http://localhost:<port>/<contextPath>/` - the port and context path come from the plugin's configuration (e.g. Tomcat plugin `port` and `path`/context root). Running `mvn tomcat7:run` starts the embedded server at that URL.

### Q4. Maven Core Concepts (5)

**Q4a) Differentiate between declaring a plugin inside the <pluginManagement> block versus declaring it directly inside the <plugins> block in pom.xml. (3)**

**Answer:**
- **`<pluginManagement>`** - a container for **plugin version and configuration** that can be *inherited* by child modules. Declaring a plugin here does **not** add it to the build; it only defines the defaults.
- **`<plugins>`** - actually **adds the plugin to the build**, so its goals are executed in the lifecycle.
- A common pattern is to lock versions in `<pluginManagement>` (parent POM) and activate the plugin in `<plugins>` (module POM).

**Q4b) Explain the purpose of the -SNAPSHOT suffix in <version>0.0.1-SNAPSHOT</version> and how Maven handles snapshot artifacts differently from release artifacts during build resolution. (2)**

**Answer:**
- `-SNAPSHOT` marks an **in-development / unstable** version that is still changing.
- Maven treats SNAPSHOTs as mutable: it can **re-check and download the latest snapshot** from a remote repository on each build.
- **Release** versions are considered fixed/final and are cached; Maven does not keep re-downloading them.

### Q5. Environment Inspection & Debugging Flags (5)

**Q5a) State the exact terminal command used to verify the JDK version detected and utilized by Maven on your machine. (2)**

**Answer:** `mvn -version` - prints Maven version **and** the Java/JDK version (plus OS info) that Maven runs on.

**Q5b) Write the single terminal command required to clean previous build outputs, execute all phases up through packaging, and produce full debug log output for troubleshooting. (3)**

**Answer:** `mvn clean package -X` - `clean` removes old output, `package` runs all phases through packaging, and `-X` (debug) prints the complete, verbose build log for diagnosis.

### Q6. Local Repository Operations & Dependency Structure (5)

**Q6a) The POM contains a dependency on a vendor library (blood-analytics.jar) that is not available in Maven Central. Write the full terminal command required to install this JAR into your local Maven cache using the coordinates specified in the POM. (3)**

**Answer:**
```
mvn install:install-file -Dfile=blood-analytics.jar -DgroupId=<groupId> -DartifactId=<artifactId> -Dversion=<version> -Dpackaging=jar
```
- `-Dfile` points to the JAR; the `-D` flags supply its coordinates; after this, Maven can resolve it as a normal local dependency.

**Q6b) Write the terminal command used to display the complete tree structure of direct and transitive dependencies for this project. (2)**

**Answer:** `mvn dependency:tree` - prints the full dependency hierarchy with scopes.

### Q7. Test Execution Controls (4)

**Q7a) Specify the standard file path locations where Maven stores: a) compiled test binary classes, b) generated JUnit test execution reports. (2)**

**Answer:** a) `target/test-classes/` - compiled test `.class` files. b) `target/surefire-reports/` - the `.txt`/`.xml` JUnit test result reports.

**Q7b) Write the exact terminal command to execute only a single test class named BloodInventoryTest. (1)**

**Answer:** `mvn -Dtest=BloodInventoryTest test`

**Q7c) Which command-line flag allows a Maven build to complete its packaging phase even if one or more unit tests fail? (1)**

**Answer:** `mvn package -Dmaven.test.failure.ignore=true` - tests run but failures do not stop the build. (`-DskipTests` / `-Dmaven.test.skip=true` instead skip running tests altogether.)

### Q8. Dependency Analysis & Scope Management (4)

**Q8a) Write the exact Maven terminal command used to analyze dependency usage and detect unused declared dependencies. (1)**

**Answer:** `mvn dependency:analyze` - reports declared-but-unused dependencies and used-but-undeclared ones.

**Q8b) Explain why the javax.servlet-api dependency is configured with <scope>provided</scope>, and state what problem occurs at runtime if this scope setting is omitted when deploying to Apache Tomcat. (3)**

**Answer:**
- The Servlet API is **provided by the servlet container** (Tomcat) at runtime; it is only needed at compile time.
- `provided` scope puts it on the **compile classpath** but **excludes it from the packaged WAR**.
- If the scope is omitted (default `compile`), the servlet JAR is bundled into `WEB-INF/lib`, causing **version conflicts/collisions** with Tomcat's own Servlet implementation at deploy time (e.g. `ClassCastException`, duplicate classes, or container startup failures).

### Part III - Dockerization and Container Management (20)

**Q1) Download a local working copy of the remote application repository, enter the project directory, and confirm that essential project configuration files exist in your root workspace. [2]**

**Answer:** `git clone <url>` -> `cd <repo>` -> `ls` to confirm `pom.xml`, `src/` and other essential files are present.

**Q2) Write a complete Dockerfile in the root directory to containerize the application using openjdk:17-jdk-slim as the base image, setting /app as the working directory, copying target/Blood-managent.jar, and defining the startup instruction to run the application. [3]**

**Answer:**
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/Blood-managent.jar app.jar
CMD ["java", "-jar", "app.jar"]
```

**Q3) Build a custom container image named Bloodbankapp-image from the current working directory. [2]**

**Answer:** `docker build -t Bloodbankapp-image .`

**Q4) Launch a container named Bloodbank-app-container running in the background, mapping host port 8080 to the container's application port 8080. [2]**

**Answer:** `docker run -d --name Bloodbank-app-container -p 8080:8080 Bloodbankapp-image`

**Q5) Display all currently running containers. [1]**

**Answer:** `docker ps`

**Q6) Display all containers regardless of whether they are running or stopped. [1]**

**Answer:** `docker ps -a`

**Q7) Enter the running Bloodbank-app-container interactively using a shell session to inspect the system environment. [2]**

**Answer:** `docker exec -it Bloodbank-app-container /bin/sh` - `-i` keeps STDIN open, `-t` allocates a terminal.

**Q8) Temporarily stop the running Bloodbank-app-container and then restart it. [2]**

**Answer:** `docker stop Bloodbank-app-container` (graceful stop) then `docker start Bloodbank-app-container` (restarts the same container, preserving its state).

**Q9) Save the state of a container with ID 0e993d2009a1 into a new image named your_dockerhub_username/Bloodbankapp:v1. [2]**

**Answer:** `docker commit 0e993d2009a1 your_dockerhub_username/Bloodbankapp:v1` - snapshots the container's changes into a reusable image.

**Q10) Authenticate your terminal session with Docker Hub. [1]**

**Answer:** `docker login` - enter your Docker Hub username and access token.

**Q11) Upload your your_dockerhub_username/Bloodbankapp:v1 to your public Docker Hub repository. [1]**

**Answer:** `docker push your_dockerhub_username/Bloodbankapp:v1`

**Q12) Terminate your session and remove stored authentication credentials from the local machine. [1]**

**Answer:** `docker logout` - clears stored Docker Hub credentials.

---

## A2. SET-6 - Sports Management System (CSE)

> **Section:** CSE - **Faculty:** S. Srija - **Paper:** SET-6 (Sports)

**Repo:** `https://github.com/sarasrija/SportManagementSystem.git` - **the paper is structurally identical to SET-5.** Use all SET-5 answers, substituting the domain names below:

| SET-5 item | SET-6 (Sports) replacement |
|---|---|
| `DonorServlet.java` (`com.bloodbank.servlet`) | `RegistrationServlet.java` (`com.sports.servlet`) |
| `DonorTest.java` (`com.bloodbank`) | `ScoreTest.java` (`com.sports`) |
| `inventory.jsp` | `schedule.jsp` |
| `BloodInventoryTest` | `TournamentBracketTest` |
| `blood-analytics.jar` | `sports-analytics.jar` |
| `target/Blood-managent.jar` | `target/sports-management.jar` |
| `Bloodbankapp-image` / `Bloodbank-app-container` | `sportsapp-image` / `sports-app-container` |
| `your_dockerhub_username/Bloodbankapp:v1` | `your_dockerhub_username/sportsapp:v1` |
| Branch `feature/donor-registration` | Branch `feature/player-registration` |
| Commit note `"Add donor registration servlet"` | `"Add player registration servlet"` |

Everything else (commands, Maven Q1-Q8, Docker steps) is exactly the same as **A1 (SET-5)**.

## A3. SET-7 - Apartment Management System (CSE)

> **Section:** CSE - **Faculty:** S. Srija - **Paper:** SET-7 (Apartment)

**Repo:** `https://github.com/sarasrija/ApartmentManagementSystem.git` - **also structurally identical to SET-5.** Use all SET-5 answers with these substitutions:

| SET-5 item | SET-7 (Apartment) replacement |
|---|---|
| `DonorServlet.java` (`com.bloodbank.servlet`) | `TenantServlet.java` (`com.apartment.servlet`) |
| `DonorTest.java` (`com.bloodbank`) | `TenantTest.java` (`com.apartment`) |
| `inventory.jsp` | `complaints.jsp` |
| `BloodInventoryTest` | `MaintenanceBillingTest` |
| `blood-analytics.jar` | `apartment-analytics.jar` |
| `target/Blood-managent.jar` | `target/apartment-management.jar` |
| `Bloodbankapp-image` / `Bloodbank-app-container` | `apartmentapp-image` / `apartment-app-container` |
| `your_dockerhub_username/Bloodbankapp:v1` | `your_dockerhub_username/apartmentapp:v1` |
| Branch `feature/donor-registration` | Branch `feature/tenant-registration` |
| Commit note `"Add donor registration servlet"` | `"Add tenant registration servlet"` |

Everything else is exactly the same as **A1 (SET-5)**.

---

# Part B - CSE Papers

## B1. SET-9 - Gym Membership Management System (CSE-B)

> **Section:** CSE-B - **Faculty:** M Nikitha - **Paper:** SET-9 (Gym Membership)

### Part I - Maven Web Project Development (40)

### Q1. Maven Project Configuration and Build (20)

**Q1a) Clone the given GitHub repository and import the project into Eclipse as a Maven Web Project. Verify that Maven recognizes the project correctly. [4]**

**Answer:**
1. **Clone the repository** - open Git Bash / terminal and run:
   - `git clone https://github.com/nikithamoturi/GymManagementSystem.git`
   - `cd GymManagementSystem`
   This downloads the full project (including `pom.xml`, `src/`, `webapp/`) to your machine.
2. **Import into Eclipse** - in Eclipse: **File -> Import -> Maven -> Existing Maven Projects -> Next -> Browse** to the project folder -> make sure `pom.xml` is ticked -> **Finish**.
3. **Verify Maven recognition** -
   - The project shows the Maven "M" icon in the Project Explorer.
   - Right-click project -> **Maven -> Update Project** -> dependencies resolve without errors.
   - Open `pom.xml` - it opens in the POM editor with no red errors.
   - Run `mvn validate` in the terminal -> **BUILD SUCCESS**.

**Q1b) Examine the pom.xml file and explain the purpose of: groupId, artifactId, version, packaging, dependencies. [5]**

**Answer:**
- **groupId** - the unique namespace that identifies the organization or group that owns the project (e.g. `com.se.lab`). It is used (with artifactId and version) to uniquely locate the artifact in repositories.
- **artifactId** - the name of the project/artifact itself (e.g. `gym-management-system`). It forms the base of the generated JAR/WAR file name and is how the project is referred to inside Maven.
- **version** - the release or development version of the artifact (e.g. `1.0-SNAPSHOT`). It distinguishes one release from another so dependencies can resolve a specific build.
- **packaging** - the type of artifact Maven produces: `jar` for a standalone Java application, `war` for a web application that runs on a servlet container such as Tomcat. Together groupId + artifactId + version are called the project coordinates (GAV).
- **dependencies** - the external libraries the application needs to compile, test and run (e.g. Servlet API, JUnit). Maven downloads these from repositories and puts them on the classpath; each dependency is declared with its own GAV.

**Q1c) Execute a Maven build and generate the deployable WAR file. Demonstrate the Maven build lifecycle phases involved in creating the WAR file and verify the generated file in the target directory. [6]**

**Answer:**
1. **Command:** `mvn clean package`
2. **What `clean` does** - deletes the existing `target/` directory so the build starts from a clean state (old compiled classes and stale artifacts are removed).
3. **Lifecycle phases executed (in order, each phase runs the previous ones):**
   - **validate** - checks the project is correct and all required information is available.
   - **compile** - compiles `src/main/java` into `.class` files stored in `target/classes`.
   - **test** - compiles and runs the JUnit tests in `src/test/java` (results in `target/surefire-reports/`).
   - **package** - packages the compiled classes and web resources into a distributable archive - for a web project this **creates the `.war` file** in `target/`.
   - *(install would also copy the artifact into the local `.m2` repository.)*
4. **Which phase generates the WAR?** - the **`package`** phase.
5. **Verify the file** - `ls target/` shows e.g. `gym-management-system-1.0-SNAPSHOT.war` (default name = `artifactId-version` unless `<finalName>` is configured).

**Q1d) Modify one suitable Maven configuration, such as the project version or final WAR name, rebuild the project, and verify the effect of the change. [5]**

**Answer:**
1. **Choose a configuration to change.**
   - Option A - change the **version**: edit `<version>1.0-SNAPSHOT</version>` to `<version>1.0</version>`.
   - Option B - change the **final WAR name**: add inside `<build>`:
     ```xml
     <build>
       <finalName>GymApp</finalName>
     </build>
     ```
2. **Why it matters** - the artifact name identifies the deployable file; `finalName` overrides the default `artifactId-version` naming and directly decides the WAR name and its URL context path on Tomcat.
3. **Rebuild** - run `mvn clean package` so the change is reflected in a fresh build.
4. **Verify the effect** - `ls target/` now shows `gym-management-system-1.0.war` (version change) or `GymApp.war` (finalName change) instead of the original name. The context path when deployed will also be `/GymApp/` (or the new version name).

### Q2. Maven Dependency and Build Analysis (20)

**Q2a) Use Maven to display the project's dependency tree. Identify the dependencies required by the web application and explain the purpose of any two dependencies. [5]**

**Answer:**
1. **Command:** `mvn dependency:tree`
2. **What it shows** - a tree of all direct and transitive dependencies with their GAV and scope (compile/test/provided), which makes it easy to see what libraries the application actually uses and how versions were resolved.
3. **Typical dependencies in this web project:**
   - `javax.servlet-api` (scope `provided`) - provides the Servlet classes (`HttpServlet`, `HttpServletRequest`, ...) that the servlets/JSPs are built on; it is *provided* because Tomcat already ships it.
   - `junit-jupiter` (scope `test`) - the JUnit 5 unit-testing framework used to write and run tests in `src/test/java`.
   - Possibly a JSP/JSTL library, a database driver (MySQL/PostgreSQL), or a logging library, depending on the project.
4. Explain any two as above (one sentence each describing what they contribute and where they are used).

**Q2b) Explain the difference between a Maven dependency and a Maven plugin. Identify one example of each from the given project. [4]**

**Answer:**
- **Dependency** = an **external library** (a JAR) that the application needs at compile/test/runtime. It is added to the project **classpath** and is written inside `<dependencies>` in `pom.xml`. Example: `javax.servlet-api`.
- **Plugin** = a **build tool / action** that Maven itself executes during the lifecycle. Plugins are not application libraries; they *do work* like compiling, testing, or packaging. They are written inside `<build><plugins>`. Example: `maven-compiler-plugin` (compiles Java source into `.class` files).
- In short: dependencies provide **libraries the code uses**; plugins perform **build steps Maven runs**.

**Q2c) Demonstrate the use of Maven commands to: remove previously generated build files; compile the project; package the application; skip or identify test execution during the build. [5]**

**Answer:**
1. **Remove previous build files:** `mvn clean` - deletes the `target/` folder.
2. **Compile the project:** `mvn compile` - compiles `src/main/java` into `target/classes` without running tests.
3. **Package the application:** `mvn package` - runs all earlier phases and produces the JAR/WAR in `target/`.
4. **Skip tests:** `mvn package -DskipTests` (compiles tests but does not run them) or `mvn package -Dmaven.test.skip=true` (does not even compile tests - fastest).
5. **Identify/run tests:** `mvn test` - compiles and executes the JUnit tests and writes reports to `target/surefire-reports/`; a failed test stops the build.

**Q2d) The project builds successfully on one system but fails on another because a required dependency cannot be resolved. Identify the possible cause and demonstrate how Maven can be used to diagnose and resolve the problem. [6]**

**Answer:**
1. **Possible causes** - the dependency's `groupId`/`artifactId`/`version` is wrong (so no system can find it), OR the JAR is simply **missing from the second machine's local `.m2` repository**, OR that machine cannot reach the repository (proxy/network/offline), OR a different Maven/JDK version resolves differently.
2. **Diagnose on the failing machine:**
   - `mvn dependency:tree` - is the dependency listed at all? Is it resolving to the expected version?
   - `mvn -X` (debug) - shows the exact repository URLs being contacted and which artifact fails to download.
   - Check the local cache: `~/.m2/repository/<groupId>/<artifactId>/<version>/` - does the JAR exist?
   - `java -version` and `mvn -version` - confirm the same JDK/Maven versions as the working machine.
3. **Resolve:**
   - Correct the coordinates/version in `pom.xml` if wrong.
   - Run `mvn clean install` to force re-download of dependencies.
   - If offline, copy the JAR or configure the repository/mirror in `settings.xml`.
4. **Prevent recurrence** - commit a working `pom.xml`, use the same Java/Maven versions across the team, and add dependencies through the central repository.

### Part II - Git & GitHub Integration (40)

### Q3. Git Branching, Modification and Commit Management (20)

**Q3a) Clone the given repository and use Git commands to display the current branch, repository status, and remote repository details. [4]**

**Answer:**
- `git clone https://github.com/nikithamoturi/GymManagementSystem.git` -> `cd GymManagementSystem`
- **Current branch:** `git branch` (or `git status`) - the active branch is marked with `*`.
- **Repository status:** `git status` - shows tracked/untracked/modified files and whether the branch is up to date.
- **Remote details:** `git remote -v` - shows the configured remote name (`origin`) with its fetch and push URLs.

**Q3b) Create a separate feature branch for modifying the membership information. Make the branch the active working branch and verify the branch using Git commands. [4]**

**Answer:**
1. Create and switch in one command: `git checkout -b feature/membership-update` (or the modern `git switch -c feature/membership-update`).
2. This creates a new pointer from the current branch and moves `HEAD` onto it, so all later commits stay isolated from `main`.
3. **Verify:** `git branch` - the new branch appears with an asterisk (`* feature/membership-update`), confirming it is active; `git status` also shows "On branch feature/membership-update".

**Q3c) Modify the membership information displayed in the application by adding Membership Type and Membership Status. Use git diff to identify and explain the changes made before committing them. [6]**

**Answer:**
1. **Make the change** - open the JSP/page that displays membership information and add two new rows/fields, e.g. `Membership Type` and `Membership Status`, keeping the same formatting as existing fields.
2. **Review with `git diff`** - this command compares the working directory with the last commit and shows each changed file with `+` (added) and `-` (removed) lines.
3. **What the diff tells you** - the `+` lines are exactly the new fields you added (e.g. `<td>Membership Type</td>` and `<td>Membership Status</td>`); if no other lines are marked, you know only the intended change was made and nothing else was accidentally touched.
4. This review-before-commit step prevents mistakes such as committing unrelated edits or half-finished code.

**Q3d) Stage the changes and create a meaningful commit. Use git log to verify the commit and explain how the commit history helps in tracking project changes. [6]**

**Answer:**
1. **Stage:** `git add .` (or `git add <page.jsp>`) - moves the changes into the staging area.
2. **Commit:** `git commit -m "Add membership type and status fields"` - a meaningful message explains *what* and *why*.
3. **Verify:** `git log --oneline` - shows the new commit at the top with its short hash and message.
4. **How commit history helps tracking:**
   - Every change is recorded with author, date and message, so you can see **who** changed **what** and **when**.
   - It acts as a timeline for auditing and code review.
   - It enables **rollback** (`git revert`/`git reset`) and **recovery** of deleted files/commits (`git reflog`).
   - It supports collaboration - teammates can understand, review and merge each other's work safely.

### Q4. Git Synchronization, Revert and Merge (20)

**Q4a) Make an additional modification to the membership information and demonstrate the difference between working-directory changes, staged changes, and committed changes using appropriate Git commands. [5]**

**Answer:**
1. **Working-directory (unstaged) change** - edit the page again (e.g. change the label text). Now the file differs from the index and the last commit.
   - `git diff` - shows **working directory vs staging area** (changes not yet staged).
2. **Staged change** - stage it with `git add .`.
   - `git diff --staged` (or `git diff --cached`) - shows **staging area vs last commit** (changes ready to be committed).
3. **Committed change** - create the commit with `git commit -m "message"`.
   - `git log` - shows the change is now permanently recorded in the repository history.
4. **Summary of the three states:** working directory (where you edit) -> staging area (what you choose for the next commit) -> repository (what is permanently saved). Git's `diff` commands let you inspect each transition.

**Q4b) Assume that the remote repository contains new commits made by another developer. Retrieve the latest remote information and update your local branch while preserving your work. Demonstrate the Git operation used. [5]**

**Answer:**
1. **If you have unpushed local commits:**
   - `git fetch origin` - downloads the new remote commits into `origin/main` without touching your branch.
   - `git rebase origin/main` - replays your local commits **on top of** the remote commits (or use the shortcut `git pull --rebase origin main`).
   - Result: your work is preserved and sits cleanly above the newest remote changes.
2. **If you have uncommitted work:**
   - `git stash` - temporarily shelves your changes.
   - `git pull origin main` - updates your branch with remote changes.
   - `git stash pop` - restores your saved work on top.
3. **Why this matters** - fetching/rebasing keeps a linear, conflict-minimal history and guarantees you do not lose local work when synchronizing.

**Q4c) Assume that one of your previous commits contains an unwanted change. Demonstrate how you would undo the commit using Git without deleting the project files from the working directory. [4]**

**Answer:**
1. **If the commit has NOT been pushed:**
   - `git reset --soft HEAD~1` - moves the branch back one commit but **keeps all changes staged**, so you can edit and recommit.
   - (Or `git reset HEAD~1` - keeps the changes in the working directory but unstaged.)
2. **If the commit has already been pushed:**
   - `git revert <commit-hash>` - creates a **new commit** that exactly reverses the bad commit, leaving history intact (safe for shared branches).
3. In both cases the project files stay on disk; nothing in your working directory is deleted.

**Q4d) Merge the completed feature branch into the main branch, resolve any merge conflict if encountered, and push the updated project to GitHub. Verify the final commit history and remote repository. [6]**

**Answer:**
1. **Switch to main:** `git checkout main` (you merge *into* the branch you are on).
2. **Merge:** `git merge feature/membership-update`.
3. **If a conflict occurs** (both branches changed the same lines):
   - `git status` - shows the conflicted file as "both modified".
   - Open the file and find the markers `<<<<<<< HEAD`, `=======`, `>>>>>>> feature/membership-update`; keep the correct code and **delete all markers**.
   - `git add <file>` - mark the conflict resolved.
   - `git commit` - complete the merge commit.
4. **Push:** `git push origin main`.
5. **Verify:**
   - `git log --oneline --graph` - shows the merge and the final history.
   - `git status` - "Your branch is up to date with 'origin/main'".
   - `git remote -v` - confirms the GitHub remote is correctly connected.

### Part III - Dockerization and Container Management (20)

### Q5. Docker Image Creation and Application Deployment (12)

**Q5a) Create a suitable Dockerfile for the Maven web application using an appropriate Java/Tomcat base image. Explain the purpose of the major instructions used in the Dockerfile. [4]**

**Answer:**
```dockerfile
FROM tomcat:9-jdk17
COPY target/gym-management-system.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- **`FROM tomcat:9-jdk17`** - sets the **base image**: a Tomcat server bundled with JDK 17, giving the container the runtime needed to run the WAR.
- **`COPY target/...war /usr/local/tomcat/webapps/`** - copies the Maven-built WAR into Tomcat's `webapps` directory, where Tomcat automatically deploys it at startup.
- **`EXPOSE 8080`** - documents that the container listens on port 8080 (Tomcat's default).
- **`CMD ["catalina.sh", "run"]`** - the command executed when the container starts; it launches the Tomcat server in the foreground (so the container stays alive).

**Q5b) Build the Maven WAR file and create a Docker image containing the web application. Verify the generated image using Docker commands. [4]**

**Answer:**
1. Build the WAR first (Docker needs the artifact to copy it): `mvn clean package`.
2. Build the image from the Dockerfile in the current directory:
   - `docker build -t gym-app:latest .` - the `-t` gives the image name:tag; the `.` is the build context.
3. **Verify the image:**
   - `docker images` - lists all local images; `gym-app` with tag `latest` should appear with its Image ID and size.

**Q5c) Run the image as a container with appropriate port mapping and verify that the Tomcat server starts successfully. [4]**

**Answer:**
1. Run the container in the background and publish the port:
   - `docker run -d -p 8080:8080 --name gym-app gym-app:latest`
   - `-d` = detached (background); `-p 8080:8080` = map host 8080 to container 8080 (format **host:container**); `--name gym-app` names the container.
2. **Verify Tomcat started:**
   - `docker ps` - the container shows status **Up**.
   - `docker logs gym-app` - shows Tomcat startup lines including "Server startup in ... ms".
   - Open `http://localhost:8080/gym-management-system/` in a browser (context path = WAR name).

### Q6. Docker Container Management and Docker Hub (8)

**Q6a) Access the application running inside the Docker container through a web browser and verify its functionality. [2]**

**Answer:** Open `http://localhost:8080/gym-management-system/` and confirm the pages load correctly (home page, registration/login, membership plans), which proves the WAR was deployed and is serving requests.

**Q6b) Display the running containers and Docker logs. Identify how these commands can be used to verify or troubleshoot a containerized application. [2]**

**Answer:**
- `docker ps` - **verifies** the container is running (status **Up**, correct port mapping).
- `docker logs gym-app` - **troubleshoots**: shows Tomcat's startup/deployment log and any exceptions, so you can diagnose crashes, 404s, or deployment failures.

**Q6c) Tag the generated image with your Docker Hub username and repository name, authenticate with Docker Hub, and push the image to the remote repository. [3]**

**Answer:**
1. Tag with your Docker Hub namespace (required for pushing): `docker tag gym-app:latest <username>/gym-app:latest`.
2. Authenticate: `docker login` -> enter your Docker Hub **username** and **personal access token**.
3. Push: `docker push <username>/gym-app:latest`.

**Q6d) Verify that the image has been successfully uploaded to Docker Hub. [1]**

**Answer:** Visit `hub.docker.com`, open your repository page, and confirm the `latest` tag/layers are listed - or run `docker search <username>/gym-app`.

---

---

## B2. SET-4 - Online Shopping Application (CSE-B)

> **Section:** CSE-B - **Faculty:** M Nikitha - **Paper:** SET-4 (Online Shopping)

### Part I - Maven Application Development (40)

### Q1. Maven Project Setup and Build (20)

**Q1a) Clone the given GitHub repository and import the project into Eclipse as a Maven project. Identify and verify the purpose of pom.xml and the main JSP. [4]**

**Answer:**
1. **Clone:** `git clone https://github.com/nikithamoturi/OnlineShoppingApp.git` -> `cd OnlineShoppingApp`.
2. **Import:** Eclipse -> **File -> Import -> Maven -> Existing Maven Projects -> Browse** -> select the folder -> tick `pom.xml` -> **Finish**; then right-click -> **Maven -> Update Project**.
3. **Purpose of `pom.xml`** - the Project Object Model: it stores the project coordinates (groupId/artifactId/version), packaging, dependencies, plugins and build configuration; Maven reads it to build the project.
4. **Purpose of the main JSP (e.g. `index.jsp`)** - the entry/landing page of the web application; it is the first page the browser loads and links to the login, registration and products pages.

**Q1b) Examine the pom.xml file and identify any two dependencies/plugins used in the project. Explain the purpose of each. [4]**

**Answer:**
- `javax.servlet-api` (dependency) - supplies the Servlet classes the web layer is written against; declared with `provided` scope because Tomcat already provides it at runtime.
- `junit-jupiter` (dependency) - the JUnit 5 framework for writing and running unit tests in `src/test/java`.
- *(Alternatively, plugins:)* `maven-compiler-plugin` - compiles Java source to bytecode; `maven-war-plugin` - packages the web app into a deployable `.war`.

**Q1c) Execute mvn clean package. If a dependency, compiler, or configuration error occurs, identify the cause, make the required changes in pom.xml, and successfully build the project. [7]**

**Answer:**
1. Run `mvn clean package`.
2. **Read the error** - Maven prints the failing plugin and cause:
   - *Dependency error* -> wrong/missing `groupId`/`artifactId`/`version`; verify against `mvnrepository.com` and fix in `<dependencies>`.
   - *Compiler error* -> `source`/`target` mismatch with installed JDK; set `<maven.compiler.source>/<target>` (or the compiler plugin) to the JDK version, e.g. 17.
   - *Configuration error* -> wrong `<packaging>`, missing plugin `<groupId>`, or XML typo (`<artificatId>`); correct the element.
3. **Rebuild** `mvn clean package` until **BUILD SUCCESS**.
4. Verify the artifact in `target/` (`ls target/*.war`).

**Q1d) Verify the generated Maven build output and execute the application on the local server. Verify that the index, login, registration, and products pages are accessible without errors. [5]**

**Answer:**
1. **Verify build output** - `ls target/` shows the WAR (e.g. `OnlineShopping-1.0-SNAPSHOT.war`).
2. **Run on the local server** - configure Tomcat in Eclipse (**Window -> Show View -> Servers -> Add server -> Tomcat**), then right-click the project -> **Run As -> Run on Server -> Finish**.
3. **Verify the pages** - open `index.jsp`, then navigate to the **login**, **registration** and **products** pages and confirm each loads without 404s or JSP compile errors; any error message points to a JSP or deployment problem to fix.

### Q2. Maven Dependency and Build Troubleshooting (20)

**Q2a) Use an appropriate Maven command to display the dependency tree and verify whether the required dependency is included in the project. [4]**

**Answer:**
- Command: `mvn dependency:tree`.
- The output lists every direct and transitive dependency with its GAV and scope in a tree structure. Search for the required dependency; if it appears, it is resolved; if not, declare/correct it in `pom.xml` and re-run.

**Q2b) Two dependencies require different versions of the same library. Explain how Maven determines which dependency version should be used. [4]**

**Answer:**
- Maven uses **dependency mediation** with the rule **"nearest definition wins"**: the version declared **closest to the project root** in the dependency tree is chosen.
- If two versions are at the **same depth**, the **first declared** dependency wins.
- To override the outcome you can use **`<dependencyManagement>`** (central version control) or **`<exclusions>`** (remove a transitive version you do not want).
- Why it matters - an unmanaged conflict can pull in an old version and cause runtime "class not found"/`NoSuchMethodError` problems.

**Q2c) Identify the location of Maven's local repository (.m2/repository) and explain how you can verify whether a required JAR file is available locally. [4]**

**Answer:**
- **Location:** `~/.m2/repository` - on Windows `C:\Users\<username>\.m2\repository`, on Linux/macOS `~/.m2/repository`.
- It stores every artifact Maven has downloaded, organized as `<groupId>` (folders) -> `<artifactId>` -> `<version>` -> the JAR.
- **Verify a JAR:** navigate to `~/.m2/repository/<groupId>/<artifactId>/<version>/` and check the `.jar` file (plus the `.pom`) exists. Alternatively `mvn dependency:tree` shows whether it resolved.
- If it is missing, run `mvn dependency:resolve` or `mvn clean install` to download it; delete the folder only if corrupted so Maven re-downloads.

**Q2d) Write suitable Maven commands to clean, compile and package the project and obtain detailed debugging information if the build fails. [4]**

**Answer:**
- `mvn clean` - delete previous build output.
- `mvn compile` - compile `src/main/java` into `target/classes`.
- `mvn package` - create the JAR/WAR artifact.
- `mvn clean package -X` - the `-X` flag enables **debug output**, printing the full log (plugin executions, download attempts, exact error), which is essential for finding the root cause of a failure.

**Q2e) If the Maven build succeeds but the application does not run correctly, state the steps you would follow to identify whether the problem is related to the Maven build, server configuration, or JSP files. [4]**

**Answer:**
1. **Maven build** - confirm the WAR was generated and is correctly structured (`jar tf <war>` shows `WEB-INF/classes`, `web.xml`); a bad package/artifact would fail here.
2. **Server configuration** - verify Tomcat is running, the WAR is deployed in `webapps`, the **context path/URL** is right, and the correct **port** is used; check Tomcat logs (`catalina.out`) for deployment errors.
3. **JSP/web files** - open each page in the browser; JSP compilation errors appear in the log and as 500 errors; fix the JSP/tag syntax or missing libraries.
4. Methodically test one layer at a time so the failing component is isolated.

### Part II - Git & GitHub Integration (40)

### Q3. Git Repository and JSP Modification (20)

**Q3a) Clone the Online Shopping repository, move into the project directory, and use suitable Git commands to verify the repository status and configured remote repository. [4]**

**Answer:**
- `git clone <url>` -> `cd OnlineShoppingApp`
- `git status` - shows the branch, any modified/untracked files and whether it is in sync with the remote.
- `git remote -v` - shows the remote name (`origin`) and the fetch/push URLs, confirming which GitHub repository it is connected to.

**Q3b) Create a new branch named feature/product-update and switch to it. Verify the currently active branch. [4]**

**Answer:**
1. `git checkout -b feature/product-update` (or `git switch -c feature/product-update`) - creates and switches in one step from the current branch.
2. This keeps your product-page work isolated from `main` until it is ready.
3. **Verify:** `git branch` - `* feature/product-update` confirms it is the active branch.

**Q3c) Modify products.jsp to display Product Category and Quantity along with the existing product information. Use git diff to display the changes made. [6]**

**Answer:**
1. **Modify** - open `products.jsp` and add the two new display fields (Product Category and Quantity), matching the existing table/formatting.
2. **Review** - `git diff` compares the working copy with the last commit:
   - Lines starting with `+` are added, `-` are removed; the file header shows which file changed.
3. **Explain the change** - the diff will show only your added category and quantity lines, confirming you did not disturb the rest of the page.
4. This is the review-before-commit habit that prevents accidental edits from being committed.

**Q3d) Stage the modified products.jsp, commit the changes with a meaningful commit message, and verify the commit. [6]**

**Answer:**
1. **Stage:** `git add products.jsp` - adds the file to the index (staging area).
2. **Commit:** `git commit -m "Add product category and quantity to products page"` - the message describes what and why.
3. **Verify:** `git log --oneline` - shows the new commit with its hash and message at the top of the branch history.
4. **Value of a meaningful message + history** - teammates can read the timeline, trace when features/bugs were introduced, revert faulty commits, and review changes accurately.

### Q4. Git Synchronization and Remote Repository (20)

**Q4a) Make a small modification to products.jsp from GitHub, such as changing the product availability label or adding simple HTML formatting. Use git diff to verify the modification before committing it. [4]**

**Answer:**
- Edit the JSP (e.g. change the "Availability" label or add an HTML tag/class), save it.
- `git diff` - shows exactly the `+`/`-` lines changed versus the last commit, so you can confirm only the intended small change is present.
- After review, `git add products.jsp` -> `git commit -m "message"`.

**Q4b) Retrieve the latest changes from the remote GitHub repository and update your local repository without losing your existing commits. Identify the appropriate Git command. [4]**

**Answer:**
- `git fetch origin` then `git rebase origin/main`, or in one command `git pull --rebase origin main`.
- `fetch` downloads the remote commits; `rebase` replays **your** commits on top of them, so nothing you committed is lost.
- (If you have *uncommitted* changes: `git stash` -> pull -> `git stash pop`.)

**Q4c) Compare the feature/product-update branch with the main branch and identify the files/commits that differ using suitable Git commands. [4]**

**Answer:**
- `git diff main feature/product-update` - shows the **file contents** that differ between the two branches.
- `git log main..feature/product-update` - lists the **commits** present in the feature branch but not in main.
- `git log --oneline --graph main feature/product-update` - gives a visual overview of divergence.
- Together these tell you exactly what will be brought in by a merge.

**Q4d) Merge the completed feature branch into the main branch, push the updated main branch to GitHub, and verify that the local and remote repositories are synchronized. [8]**

**Answer:**
1. **Switch to main:** `git checkout main`.
2. **Merge:** `git merge feature/product-update` - Git fast-forwards (if main hasn't moved) or creates a merge commit.
3. **If conflict** - `git status` shows the conflicted file; open it, delete the `<<<<<<<`/`=======`/`>>>>>>>` markers keeping the correct code, `git add <file>`, then `git commit`.
4. **Push:** `git push origin main`.
5. **Verify synchronization:**
   - `git status` -> "Your branch is up to date with 'origin/main'".
   - `git log --oneline --graph` -> shows the merged history.
   - `git fetch` then `git status` again - if up to date, local and remote point at the same commit.
6. Why it matters - synchronized branches avoid merge conflicts and keep the shared repository as a single source of truth.

### Part III - Containerization and Container Management (20)

### Q5. Dockerfile and Application Containerization (12)

**Q5a) Create a suitable Dockerfile for the Maven-based web application. Select an appropriate Java/Maven base image, set the working directory, and copy the project files into the container. [3]**

**Answer:**
```dockerfile
FROM maven:3.9-eclipse-temurin-17
WORKDIR /app
COPY . /app
```
- `FROM maven:3.9-eclipse-temurin-17` - a base image containing Maven + JDK 17, so the container can build the project.
- `WORKDIR /app` - sets the working directory for all subsequent commands.
- `COPY . /app` - copies the whole project (including `pom.xml` and `src/`) into the container.

**Q5b) Configure the Dockerfile to build the Maven project and deploy the generated WAR file into the appropriate Apache Tomcat webapps directory. [4]**

**Answer:**
```dockerfile
# Build stage
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app
COPY . /app
RUN mvn clean package

# Runtime stage
FROM tomcat:9-jdk17
COPY --from=build /app/target/OnlineShopping.war /usr/local/tomcat/webapps/
```
- The **build stage** compiles and packages the project (`mvn clean package`).
- The **runtime stage** uses a Tomcat image and copies the WAR from the build stage into `webapps`, where Tomcat auto-deploys it.

**Q5c) Expose the appropriate Tomcat port and configure the container to start the Tomcat server. [2]**

**Answer:**
```dockerfile
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- `EXPOSE 8080` documents the port; `CMD` starts the Tomcat server in the foreground so the container keeps running.

**Q5d) Build a Docker image named OnlineShopping with a suitable tag and verify that the image has been created successfully. [3]**

**Answer:**
- `docker build -t onlineshopping:1.0 .` - builds from the Dockerfile in the current directory (`.`), tagging the image `onlineshopping:1.0`.
- **Verify:** `docker images` - the image appears with its tag, Image ID and size.

### Q6. Run, Verify and Push Docker Image (8)

**Q6a) Run the OnlineShopping image as a Docker container by mapping host port 8080 to container port 8080. Verify that the container is running. [3]**

**Answer:**
- `docker run -d -p 8080:8080 --name online-shopping onlineshopping:1.0`
- `-d` detached, `-p 8080:8080` = host:container port mapping, `--name` gives it a name.
- **Verify:** `docker ps` - the container is listed with status **Up** and the mapping `0.0.0.0:8080->8080/tcp`.

**Q6b) Access the application through http://localhost:8080 and verify that the Online Shopping application is running successfully. [2]**

**Answer:** Open `http://localhost:8080/OnlineShopping/` (context path = WAR name) in a browser; if the index/login/registration/products pages render, the application is deployed and running.

**Q6c) Tag the OnlineShopping image using your Docker Hub username and repository name, log in to Docker Hub, and push the image. [2]**

**Answer:**
- `docker tag onlineshopping:1.0 <username>/onlineshopping:1.0` - adds the Docker Hub namespace required for pushing.
- `docker login` - authenticate (username + access token).
- `docker push <username>/onlineshopping:1.0` - upload the image to Docker Hub.

**Q6d) Verify that the Docker image is available in your Docker Hub repository. [1]**

**Answer:** Check `hub.docker.com` (your repository page) or run `docker search <username>/onlineshopping`.

---

---

## B3. SET-2 - E-Ticketing System (CSE-A)

> **Section:** CSE-A - **Faculty:** K Yasaswini - **Paper:** SET-2 (E-Ticketing)

**Main task:** Clone `https://github.com/ssvkotamraju/E-ticketing.git`, import into Eclipse, fix `pom.xml`, make a successful build. Resolve dependencies (10), build WAR/JAR (8), verify artifact in `target/` (2).

**Q) Explain the steps required to clone the repository and import the project into Eclipse. [4]**

**Answer:**
1. `git clone https://github.com/ssvkotamraju/E-ticketing.git` - downloads the project to your machine.
2. `cd E-ticketing` - move into the project folder.
3. In Eclipse: **File -> Import -> Maven -> Existing Maven Projects -> Next -> Browse** to the folder -> ensure `pom.xml` is selected -> **Finish**.
4. Eclipse reads the POM, downloads dependencies (visible in the console/progress), and builds the Maven project model; right-click -> **Maven -> Update Project** to refresh if needed.

**Q) After importing, several dependency-related errors are displayed. How would you identify and resolve the Maven dependency problems? [6]**

**Answer:**
1. **Identify** - right-click project -> **Maven -> Update Project** to refresh the model; open `pom.xml` and check the `<dependencies>` block; look for errors in the Problems view.
2. **Check coordinates** - verify each dependency's `groupId`, `artifactId` and `version` against `mvnrepository.com`; a typo or outdated version is the most common cause.
3. **Resolve** - correct the coordinates/versions, save, and re-run `mvn clean install` (or `mvn dependency:resolve`).
4. **Debug if still failing** - `mvn -X` prints debug output showing which artifact fails and from which repository.
5. Check the local cache `~/.m2/repository` for the expected JARs.

**Q) The project fails to compile because the Java compiler configuration in pom.xml does not match the Java version installed on your system. How would you troubleshoot and correct the configuration? [6]**

**Answer:**
1. **Check installed JDK:** `java -version`.
2. **Check which JDK Maven uses:** `mvn -version` (shows Java version Maven runs on).
3. **Compare** - if the POM's `source`/`target` is higher (or lower) than the installed JDK, Maven rejects it (e.g. "Source option X is no longer supported").
4. **Fix in `pom.xml`** - set the version to match the installed JDK:
   ```xml
   <properties>
     <maven.compiler.source>17</maven.compiler.source>
     <maven.compiler.target>17</maven.compiler.target>
   </properties>
   ```
   or configure the `maven-compiler-plugin` `source`/`target`.
5. Rebuild with `mvn clean compile` and confirm BUILD SUCCESS.

**Q) You execute mvn clean install, but the build fails during the compilation phase. Explain how you would use the Maven error output to identify the root cause. [4]**

**Answer:**
1. Read the `[ERROR]` section - it names the failing plugin (usually `maven-compiler-plugin`) and shows the **file and line number** of the compilation error.
2. Distinguish the error type: a *compiler* error (syntax/type in `.java`) vs a *resolution* error (missing dependency).
3. Fix accordingly (correct the Java code, or fix the dependency/version), then re-run `mvn clean install`.
4. If the cause is not obvious, add `-X` for full debug output showing every step of the build.

**Q) The E-Ticketing application needs to be deployed as a web application, but Maven generates an unexpected package type. Which section of pom.xml would you inspect and modify? [4]**

**Answer:**
- Inspect the `<packaging>` element (directly under `<project>`).
- The default (when omitted) is `jar`. For a web application that deploys to Tomcat, set `<packaging>war</packaging>`.
- This changes the artifact type: Maven's war plugin then creates a `.war` with the `WEB-INF/web.xml` structure instead of a plain `.jar`.
- After the change, rebuild with `mvn clean package` and verify a `.war` is produced in `target/`.

**Q) After modifying pom.xml, the application behaves differently from the previous build. Explain why executing a clean Maven build can help and which Maven command you would use. [4]**

**Answer:**
- Old compiled `.class` files, stale resources and previously packaged artifacts remain in `target/` and can be reused by an incremental build, causing mismatched/old behavior.
- `mvn clean` deletes the entire `target/` directory so the next build recompiles everything from source with the new POM settings.
- Command: `mvn clean package` (or `mvn clean install`).
- This guarantees a reproducible build that matches the current `pom.xml`.

**Q) Maven displays BUILD SUCCESS, but the E-Ticketing application does not open correctly in the browser. What additional checks would you perform? [4]**

**Answer:**
1. **Deployment** - confirm the WAR is present in Tomcat's `webapps` directory and Tomcat actually deployed it (look for `e-ticketing` folder / log line).
2. **URL/context path** - use the correct address `http://localhost:8080/e-ticketing/` (context path = WAR name).
3. **Server** - confirm Tomcat is running, on the expected port, and check `catalina.out`/logs for errors.
4. **Application** - open individual JSPs; JSP compile errors or missing runtime dependencies appear as 500 errors in the logs.

**Q) The development team wants a quick production package because all tests were already executed successfully in the CI pipeline. Which Maven command could be used to avoid running tests during packaging? [4]**

**Answer:**
- `mvn package -DskipTests` - skips running the tests (but still compiles them), producing the package faster.
- Or `mvn package -Dmaven.test.skip=true` - skips both compiling and running tests (fastest).
- This is safe here because CI already validated the tests.

**Q) The build fails because Maven cannot download a dependency. How would you determine whether the problem is caused by the dependency declaration, repository configuration, or network connectivity? [4]**

**Answer:**
1. **Declaration** - run `mvn dependency:tree` (or `mvn dependency:get -Dartifact=<groupId>:<artifactId>:<version>`); if it can't even find the artifact, the coordinates are likely wrong.
2. **Repository configuration** - check `<repositories>` in `pom.xml` and `<mirrors>`/`<proxies>` in `~/.m2/settings.xml`; a wrong/blocked repository URL prevents downloads.
3. **Network connectivity** - run `mvn -X` (shows each download attempt and error), test connectivity/ping to the repository host, check proxy settings and firewall.
4. Fix whichever layer failed (correct coordinates, fix repository/mirror, resolve network/proxy) and rebuild.

**Q) You have fixed the ticket-booking calculation logic and want Maven to execute the project's tests. Which Maven command would you use? [4]**

**Answer:**
- `mvn test` - compiles and runs the unit tests in `src/test/java` and writes reports to `target/surefire-reports/`.
- Or `mvn clean test` to start from a clean state.
- The build fails if any test fails, confirming the fix works.

### Part II - Git & GitHub (40)

**Task: The project is not under version control. Initialize Git, set global config, and push the Maven project to GitHub. [5]**

**Answer:**
1. `git init` - initialize a new Git repository.
2. `git add .` - stage all project files.
3. `git commit -m "Initial commit"` - first commit.
4. `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"` - set author identity.
5. Create an empty repository on GitHub, then `git remote add origin <url>` and `git push -u origin main` (the `-u` sets upstream tracking).

**Q) You receive the railway ticket-booking project as a local folder that is not under Git version control. How would you create the first commit? [4]**

**Answer:**
1. `git init` - turn the folder into a repository.
2. `git add .` - stage everything.
3. `git commit -m "Initial commit"` - record the first snapshot.
4. Optionally set `git config --global user.name/email` first so the commit has an author.

**Q) The portal needs a new feature that allows users to search trains based on source and destination. Explain how you would create a separate branch and develop this feature without directly modifying main. [4]**

**Answer:**
1. Create and switch: `git checkout -b feature/train-search` (from `main`).
2. Develop the feature on this branch, staging and committing as usual (`git add .`, `git commit -m "..."`).
3. `main` remains untouched and stable; the new feature is isolated until tested.
4. When complete, merge back: `git checkout main` -> `git merge feature/train-search`.

**Q) You have modified the ticket-booking page and added a new CSS file. You want to review the changes before committing them. Which Git commands would you use? [4]**

**Answer:**
- `git status` - shows which files are modified (`M`) and which are new/untracked (`??`), i.e. the CSS file.
- `git diff` - shows the actual line-by-line changes of the modified page (working directory vs index).
- Review these, then stage and commit.

**Q) You accidentally modify the train-search page and want to discard the changes because they have not yet been committed. Which Git command would you use? [4]**

**Answer:**
- `git restore <file>` (or the older `git checkout -- <file>`) - restores the file to the last committed version, discarding all uncommitted edits.
- If many files: `git restore .` (careful - it is irreversible).
- Staged-but-unwanted files can be unstaged with `git restore --staged <file>` before discarding.

**Q) You have created several local commits while experimenting with the ticket-booking functionality. None of the commits have been pushed. You want to move your branch back to an earlier commit. [4]**

**Answer:**
- `git log --oneline` - find the target commit hash.
- `git reset --soft <hash>` - moves the branch pointer back but **keeps all later changes staged** (safe, work preserved).
- `git reset <hash>` (mixed) - moves back and keeps changes **unstaged** in the working directory.
- `git reset --hard <hash>` - moves back and **discards** all changes (use only if you really want to lose them).

**Q) Several developers have created temporary branches for completed features. The branches are no longer required after their changes have been merged. How would you identify and delete the unused branches? [4]**

**Answer:**
1. **Identify merged branches:** `git branch --merged` - lists branches fully contained in the current branch (safe to delete).
2. **Delete:** `git branch -d <branch>` - safe delete (Git refuses if the branch has unmerged changes).
3. **Force delete:** `git branch -D <branch>` - for unmerged branches you no longer need.
4. Clean up multiple at once: `git branch -d b1 b2 b3`.

**Q) Developer A implements train-search while Developer B implements passenger-registration, both on separate branches. Explain how you would merge them into the main development branch. [4]**

**Answer:**
1. `git checkout main` - you merge *into* the current branch.
2. `git merge feature-train-search` - bring in Developer A's work.
3. `git merge feature-passenger-registration` - bring in Developer B's work.
4. If either merge reports conflicts, resolve them (edit file, remove markers, `git add`, `git commit`) before the next merge; push when done.

**Q) A teammate cannot directly push to your repository but sends you their changes as a Git patch. Explain how you would create, inspect, and apply the patch. [4]**

**Answer:**
1. **Create** (the sender side): `git format-patch -1 <commit-hash>` - produces `0001-*.patch`; `git format-patch -3` for the last 3 commits.
2. **Inspect** (receiver side): `git apply --check <patch>` - dry-run to see if it applies cleanly; you can also open the `.patch` file.
3. **Apply:** `git apply <patch>` - applies to the working tree without a commit; or `git am <patch>` - applies and recreates the original commit (author/message preserved).

**Q) You receive a patch from a teammate, but the patch cannot be applied cleanly because your local version contains conflicting changes. How would you troubleshoot and resolve the problem? [4]**

**Answer:**
1. Run `git apply --check` to see the failure reason (context no longer matches - your file differs from the patch's base).
2. Align bases: `git fetch origin` and `git rebase origin/main` so your branch matches the branch the patch was made against.
3. Retry `git apply --check`; if it now passes, apply normally.
4. If still conflicting, use `git apply --3way` (or `--reject`) and fix the rejected hunks manually, then `git add` the file.

**Q) The railway ticket-booking application has been tested successfully. You now need to upload the project and its Git history to your GitHub repository. Explain how you would configure the remote repository and push the required branch. [4]**

**Answer:**
1. Create an **empty** repository on GitHub (do not add README, or push will conflict).
2. `git remote add origin <url>` - connect local to remote.
3. `git push -u origin main` - uploads the branch **with its full commit history**.
4. `git push -u origin main` also sets upstream, so later you can simply run `git push`/`git pull`.

### Part III - Docker (20)

**Task i) Create a Dockerfile and build a Docker image named OTS to push it to Docker Hub. ii) Run the image in a container and expose port 8080. Check if the app runs at http://localhost:8080. [20]**

**Answer:**
```dockerfile
FROM tomcat:9-jdk17
COPY target/e-ticketing.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- Build the WAR: `mvn clean package`.
- Build image: `docker build -t ots:latest .`
- Push to Docker Hub: `docker tag ots:latest <username>/ots:latest` -> `docker login` -> `docker push <username>/ots:latest`
- Run: `docker run -d -p 8080:8080 --name ots ots:latest`
- Check `http://localhost:8080/e-ticketing/`.

**Qa) You execute docker build, but Docker reports an error while creating the OTS image. What steps would you follow to identify and correct the problem? [4]**

**Answer:**
1. **Read the build error** - Docker stops at the failing instruction and prints the line number and reason.
2. **Check the Dockerfile** - directive names and syntax must be correct (`FROM`, `COPY`, `EXPOSE`, `CMD`).
3. **Check the build context** - the `.` must be the project root, and any file in `COPY` must exist inside it (e.g. run `mvn clean package` first so `target/e-ticketing.war` exists).
4. **Check the base image** - `tomcat:9-jdk17` must be a valid, pullable image (`docker pull tomcat:9-jdk17`).
5. Fix the issue and re-run `docker build`.

**Qb) The E-Ticketing application listens on port 8080 inside the container, but localhost:8080 cannot access it. Explain how Docker port mapping should be configured. [4]**

**Answer:**
- Containers are isolated: a port open inside the container is **not automatically** reachable from the host.
- You must **publish** the port with the `-p HOST:CONTAINER` flag when running: `docker run -d -p 8080:8080 --name ots ots:latest`.
- Here host port 8080 is mapped to container port 8080, so `http://localhost:8080` reaches the app.
- If you wanted host 8080 -> container 8082 you would write `-p 8080:8082` (host on the left, container on the right).

**Qc) The OTS Docker image builds successfully, but the container stops immediately after it starts. What commands or logs would you inspect to determine the cause? [4]**

**Answer:**
1. `docker ps -a` - shows the container with an **Exit code** (0 = clean exit, non-zero = error).
2. `docker logs <container>` - the main diagnostic: shows the process output/stack trace that caused the crash.
3. `docker inspect <container>` - check the `CMD`/`ENTRYPOINT`; a missing/wrong startup command makes the container exit at once.
4. Common causes & fixes: WAR not copied (fix `COPY` path), missing `CMD` (add `["catalina.sh","run"]`), or the app needs a DB/network that is unavailable.

**Qd) The E-Ticketing application works on one developer's computer but fails on another because of differences in Java and server configurations. Explain how Docker can solve this problem. [4]**

**Answer:**
- The classic "works on my machine" problem happens because Java version, Tomcat version, paths and OS settings differ between machines.
- Docker packages the application **together with its entire runtime** (JDK 17, Tomcat, libraries) into one image.
- Every container created from that image runs the **exact same configuration**, regardless of the host OS.
- So deployment becomes consistent and reproducible: build once, run anywhere.

**Qe) The application generates a .war file after running Maven. You need to deploy this WAR file inside a Tomcat-based Docker container and make the application available on port 8080. What changes would you make to the Dockerfile? [4]**

**Answer:**
```dockerfile
FROM tomcat:9-jdk17
COPY target/e-ticketing.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- Use a **Tomcat base image** (provides the servlet container).
- `COPY` the WAR into Tomcat's `webapps` folder (Tomcat auto-deploys it).
- `EXPOSE 8080` and start Tomcat with `CMD`.
- Then `docker build -t ots:latest .` and `docker run -d -p 8080:8080 ots:latest`; access `http://localhost:8080/e-ticketing/`.

---

---

## B4. Set-1 (2) - Metro Booking System (CSE-G)

> **Section:** CSE-G - **Faculty:** Anuj - **Paper:** Set-1 (2) (Metro Booking)

**Main task:** Clone `https://github.com/anujyog1/MetroRepo.git`, fix `pom.xml`, build successfully.
- **Resolve dependencies using `pom.xml` (10)** - ensure correct coordinates/versions and scopes; run `mvn clean install` to download.
- **Build the project to generate WAR/JAR (8)** - `mvn clean package` (runs validate -> compile -> test -> package).
- **Verify the generated artifact in `target/` (2)** - `ls target/` shows the `.war`/`.jar`.

### Part I - Maven Scenario Questions (10 x 2 = 20)

**Q1) How do you explicitly force Maven to ignore the unwanted transitive version? [2]**

**Answer:** Exclude it inside the dependency that pulls it in:
```xml
<dependency>
  <groupId>com.example</groupId>
  <artifactId>metro-core</artifactId>
  <version>1.0</version>
  <exclusions>
    <exclusion>
      <groupId>unwanted.group</groupId>
      <artifactId>unwanted-lib</artifactId>
    </exclusion>
  </exclusions>
</dependency>
```

**Q2) A dependency you added is not recognized by the compiler. What steps would you take to confirm it is available in .m2 and listed in dependency tree? [2]**

**Answer:** `mvn dependency:tree` (is it listed?); check `~/.m2/repository/<groupId>/<artifactId>/<version>/` for the JAR; if missing run `mvn dependency:resolve` / `mvn clean install`; fix coordinates if wrong.

**Q3) You need to change your Java application from a WAR to a standalone JAR. What pom.xml changes are needed? [2]**

**Answer:** Change `<packaging>war</packaging>` -> `<packaging>jar</packaging>`; remove web-only dependencies if no longer used; optionally add `maven-jar-plugin` with `<mainClass>` so `java -jar` works.

**Q4) How do you build a Java project using Maven, and what files are generated in the target/ folder after running mvn clean install? [2]**

**Answer:** Run `mvn clean install`. In `target/` you get `classes/` (compiled `.class`), `generated-sources/`, `surefire-reports/` (test results) and the final `jar`/`war`; `install` also copies the artifact into `~/.m2/repository`.

**Q5) How do you create a Maven web project that packages into a WAR file, and what is the standard folder structure for such a project? [2]**

**Answer:** Structure: `src/main/java`, `src/main/resources`, `src/main/webapp` (`WEB-INF/web.xml` + JSPs), `pom.xml` with `<packaging>war</packaging>`; create it with the `maven-archetype-webapp` archetype.

**Q6) How do you configure a Maven web project, and how does its packaging and execution differ from a traditional WAR-based application? [2]**

**Answer:** Configure via `<packaging>` and web plugins. A **JAR** runs standalone with `java -jar`; a **WAR** must be deployed to and executed by a servlet container (Tomcat).

**Q7) You need to build your project with production database configurations (prod profile) and skip running unit tests to save time during deployment. [2]**

**Answer:** `mvn clean package -Pprod -DskipTests` - `-Pprod` activates the production profile (defined in `<profiles>`), `-DskipTests` skips test execution.

**Q8) Which Maven command displays the full dependency hierarchy? [2]**

**Answer:** `mvn dependency:tree`

**Q9) The compile phase only compiles Java source code into .class files. Packaging into a .jar happens in the package phase. [2]**

**Answer:** Correct. `mvn compile` produces `.class` files in `target/classes`; `mvn package` bundles them into the `.jar`/`.war` in `target/`.

**Q10) You updated code in your project, but when you run mvn package, old compiled files in the target/ folder cause build errors. What command deletes old build output before compiling fresh code? [2]**

**Answer:** `mvn clean package` - the `clean` phase deletes the old `target/` first.

### Part II - Git & GitHub (40)

**Task: Initialize a Git repository and add the Maven project files. [5]**

**Answer:** `git init` -> `git add .` -> `git commit -m "Initial commit"`.

**Task: Set global config, and push your Maven project to GitHub. [5]**

**Answer:** `git config --global user.name "Name"` and `git config --global user.email "email"`; create an empty repo on GitHub; `git remote add origin <url>`; `git push -u origin main`.

**Q1) How do you verify which remote URL your local repository is connected to, and how would you rename the remote default from origin to metro-origin? [2]**

**Answer:** `git remote -v` (see URLs) then `git remote rename origin metro-origin`.

**Q2) You need to create a new branch called feature/fare-calculator directly from the main branch and switch to it in a single command. [2]**

**Answer:** `git checkout -b feature/fare-calculator` (from main).

**Q3) Developer A modified TicketController.java on main while you modified the exact same lines on feature/qr-scanner. Which conflict arises and how do you resolve it? [2]**

**Answer:** A content (edit-edit) merge conflict. Resolve: `git status` -> open the file -> remove `<<<<<<<`/`=======`/`>>>>>>>` markers keeping the correct code -> `git add TicketController.java` -> `git commit` (or `git rebase --continue`).

**Q4) A commit containing incorrect fare calculation logic was accidentally pushed to remote main. Others have already pulled, so you cannot rewrite history. Which Git command safely undoes the changes while creating a new commit? [2]**

**Answer:** `git revert <commit-hash>` -> `git push origin main`.

**Q5) The base ticket fare in FareMatrix.json was changed incorrectly. How do you inspect the line-by-line commit history of FareMatrix.json to determine who modified a specific line, when, and in which commit? [2]**

**Answer:** `git blame FareMatrix.json` - shows commit hash, author, and date for every line.

**Q6) You modified Booking register.jsp; how do you push it to GitHub? Give all steps. [2]**

**Answer:** `git status` -> `git add register.jsp` -> `git commit -m "Update booking registration page"` -> `git push origin main`.

**Q7) You pushed a wrong change in register.jsp. How do you undo the commit but keep the history clean? [2]**

**Answer:** `git revert <commit-hash>` -> `git push origin main` - a new undo commit, history untouched.

**Q8) While staging with git add ., you accidentally staged db_passwords.env containing secrets. You haven't committed yet. How do you remove it from the staging area without deleting the actual file? [2]**

**Answer:** `git restore --staged db_passwords.env` (or `git reset HEAD db_passwords.env`); then add `db_passwords.env` to `.gitignore`.

**Q9) You want to know who last modified login.jsp. [2]**

**Answer:** `git blame login.jsp` (line-by-line authorship) or `git log --oneline login.jsp` (commit history of the file).

**Q10) How do you see the full details (author, date, changes) of the last commit? [2]**

**Answer:** `git show HEAD` (or `git log -1 -p`) - author, date, message and the diff.

**Extra (5 marks): How do you temporarily save your uncommitted changes without making a messy commit, switch to main, fix the bug, switch back to your feature branch, and restore your saved work?**

**Answer:**
1. `git stash` - save your uncommitted changes and clean the working tree.
2. `git checkout main` - switch to main; fix the bug and commit it.
3. `git checkout feature-branch` - return to your feature work.
4. `git stash pop` - restore your saved changes.

**Extra (5 marks): In case of merge conflict, how do you identify which files are conflicting, resolve the conflict and successfully complete the merge process? Illustrate using Git commands.**

**Answer:**
1. `git status` - identifies the conflicted file(s), marked "both modified".
2. Open the file and find the markers `<<<<<<< HEAD`, `=======`, `>>>>>>> <branch>`; edit to keep the desired code and delete all markers.
3. `git add <file>` - mark it resolved.
4. `git commit` - complete the merge commit.
5. `git push origin main` - publish the merged result.

### Part III - Docker (20)

**Task: Dockerfile creation (3) - ensure it copies the WAR/JAR and runs on Tomcat.**

**Answer:**
```dockerfile
FROM tomcat:9-jdk17
COPY target/metro-repo.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

**Task: Image building and run (4).**

**Answer:** `docker build -t metro-app:latest .` -> `docker run -d -p 8080:8080 --name metro-app metro-app:latest`.

**Task: Push to Docker Hub (5) - tag and push the created image.**

**Answer:** `docker tag metro-app:latest <username>/metro-app:latest` -> `docker login` -> `docker push <username>/metro-app:latest`.

**Q1) How do you run the PostgreSQL database service in a detached Docker container named metro-db using port 5432? [1]**

**Answer:** `docker run -d --name metro-db -p 5432:5432 postgres`

**Q2) How do you map the host machine's port 80 to Tomcat's internal port 8082 when starting the container metro-app? [1]**

**Answer:** `docker run -d -p 80:8082 --name metro-app metro-app:latest`

**Q3) How do you view the real-time application metro-app logs to see what error was thrown? [1]**

**Answer:** `docker logs -f metro-app` - the `-f` streams the log live.

**Q4) You updated the ticket calculation logic and recompiled the WAR, but the running container still has the old version. What commands do you run to update it? [1]**

**Answer:**
- `docker build -t metro-app:latest .` (rebuild image with the new WAR)
- `docker stop metro-app` -> `docker rm metro-app`
- `docker run -d -p 8080:8080 --name metro-app metro-app:latest`

**Q5) How can you launch an interactive terminal inside the running container to inspect its internal file system? [1]**

**Answer:** `docker exec -it metro-app /bin/sh`

**Q6) What Docker command instantly cleans up all unused images, stopped containers, and builds cache layers? [1]**

**Answer:** `docker system prune -a` (add `-f` to skip the confirmation prompt).

**Q7) How do you run the Metro container in the background so your terminal remains free and the app keeps running? [1]**

**Answer:** `docker run -d ...` - detached mode.

**Q8) What flag allows you to forcefully stop and remove a running container in a single line? [1]**

**Answer:** `docker rm -f <container>` - force-removes even if running.

---

---

## B5. Set-4 (2) - Online Boutique Store (Haleema, SET-III)

> **Section:** CSE (branch not stated in the paper) - **Faculty:** Haleema - **Paper:** Set-4 (2) (Online Boutique Store)

### Part I - Maven Java Application Development (40)

**Q1) Clone the Online Boutique Store Maven project from GitHub. [4]**

**Answer:**
- `git clone https://github.com/haleema91/Internal-1-OBS.git` - downloads the project.
- `cd Internal-1-OBS` - move into the folder; verify `pom.xml` and `src/` exist (`ls`).

**Q2) Open the pom.xml and identify all the errors in the Maven configuration that may prevent the project from building successfully. [6]**

**Answer:**
Likely configuration errors to find and fix:
1. **Wrong/missing `<packaging>`** - should be `war` for a web app (default is `jar`).
2. **Incorrect dependency coordinates/versions** - wrong `groupId`/`artifactId`/`version`, or a version that does not exist.
3. **Compiler settings** - `source`/`target` set to an unsupported old Java (e.g. 5) -> "Source option 5 is no longer supported".
4. **Missing plugin `<groupId>`** - e.g. a plugin declared with only `artifactId` + `version` cannot be resolved.
5. **XML errors** - typos such as `<artificatId>`, unclosed tags, wrong nesting.
6. **Missing/incomplete dependencies** - e.g. no Servlet API for a web app, JUnit without `<version>`.
Fix each, then `mvn clean package` until BUILD SUCCESS.

**Q3) Build and run the Online Boutique Store Maven project successfully. Which Maven commands will you use? [5]**

**Answer:**
1. `mvn clean` - remove old build output.
2. `mvn compile` - compile the sources.
3. `mvn test` - run unit tests.
4. `mvn package` - create the JAR/WAR artifact; verify with `ls target/`.
5. For a web app: deploy the WAR to Tomcat (Eclipse **Run on Server**) and open it in the browser. (`mvn clean install` also installs to the local `.m2`.)

**Q4) The application is currently packaged as a WAR, but the company wants to run it as a standalone Java application. What changes should be made in the pom.xml to convert it to a JAR application? [5]**

**Answer:**
1. Change `<packaging>war</packaging>` -> `<packaging>jar</packaging>`.
2. Remove or keep only needed dependencies - drop web-only ones (Servlet/JSP/Tomcat) if the app no longer needs them.
3. To make it **executable**, add the `maven-jar-plugin` with the main class:
   ```xml
   <plugin>
     <groupId>org.apache.maven.plugins</groupId>
     <artifactId>maven-jar-plugin</artifactId>
     <configuration>
       <archive>
         <manifest>
           <mainClass>com.boutique.Main</mainClass>
         </manifest>
       </archive>
     </configuration>
   </plugin>
   ```
4. Rebuild: `mvn clean package`; run with `java -jar target/<name>.jar`.

**Q5) The Online Boutique Store needs to connect to a MySQL database. The required library is not available. How would you add the dependency, and which Maven command would you use to download it? [4]**

**Answer:**
1. Add to `<dependencies>` in `pom.xml`:
   ```xml
   <dependency>
     <groupId>mysql</groupId>
     <artifactId>mysql-connector-java</artifactId>
     <version>8.0.33</version>
   </dependency>
   ```
2. Maven **downloads it automatically** the next time the project builds (dependency resolution).
3. To force/verify the download: `mvn dependency:resolve` or `mvn clean install`; confirm it in `~/.m2/repository` and with `mvn dependency:tree`.

**Q6) Building with a newer JDK gives "Source option 5 is no longer supported / Target option 5 is no longer supported". Which section of pom.xml would you modify, and which plugin is responsible for Java compilation? [3]**

**Answer:**
- Modify the **compiler configuration** - either the `<properties>` with `<maven.compiler.source>`/`<maven.compiler.target>` (set to your JDK, e.g. 17), or the `maven-compiler-plugin` `<configuration>` `<source>`/`<target>`.
- The plugin responsible is **`maven-compiler-plugin`**.

**Q7) The application fails to build because Maven cannot resolve a dependency; you suspect the groupId, artifactId, or version is incorrect. What would you check, and which Maven commands could help troubleshoot? [3]**

**Answer:**
1. Check the `<dependency>` block against `mvnrepository.com` - confirm correct `groupId`/`artifactId`/`version`.
2. `mvn dependency:tree` - see whether/which version is resolved.
3. `mvn -X` - debug output shows the exact resolution failure.
4. Check `~/.m2/repository` for the JAR; correct the coordinates and rebuild.

**Q8) Update the project version from 1.0-SNAPSHOT to 1.0. What would you change, and what is the difference between a SNAPSHOT version and a release version? [2]**

**Answer:** Change `<version>1.0-SNAPSHOT</version>` -> `<version>1.0</version>`. **SNAPSHOT** = in-development/unstable (Maven re-resolves it from repos); **release** = stable/final (cached).

**Q9) A new developer wants to see which external libraries are used. Which Maven command would you use? [3]**

**Answer:** `mvn dependency:tree` - lists all direct and transitive dependencies with versions and scopes; `mvn dependency:analyze` additionally flags unused ones.

**Q10) Push the completed Online Boutique Store Maven project to GitHub and share it with your teammate. Write the required Git commands. [5]**

**Answer:**
1. `git init` - initialize the repository.
2. `git add .` - stage all files.
3. `git commit -m "Initial commit"` - first commit.
4. Create an empty repo on GitHub; `git remote add origin <url>`.
5. `git push -u origin main` - upload code + history; share the repository URL with the teammate.

### Part II - Git & GitHub Integration (40)

**Q1) Verify whether the local project is connected to the correct GitHub repository; view the configured remote URL and identify the remote name. [4]**

**Answer:**
- `git remote -v` - shows each remote name (e.g. `origin`) with its fetch and push URLs.
- Confirm the URL matches the expected `Internal-1-OBS` repository.
- If wrong, update with `git remote set-url origin <new-url>`.

**Q2) Create a new branch named product-search and switch to it without making changes directly to main. [3]**

**Answer:** `git checkout -b product-search` (from main) - creates and activates the branch; all commits stay isolated from `main`.

**Q3) You modified Product.java and Order.java. Which Git command shows the exact lines changed versus the last committed version? [3]**

**Answer:** `git diff` - shows working-directory vs last commit, line by line (`+` added, `-` removed). Use `git diff --staged` after staging.

**Q4) While modifying Customer.java you deleted important code; the file is not committed. Which Git command discards your local changes and restores Customer.java? [4]**

**Answer:**
- `git restore Customer.java` (or the older `git checkout -- Customer.java`) - restores the file from the last commit, discarding all uncommitted edits.
- This is safe here because nothing was committed; be careful because the discard is permanent.

**Q5) Your teammate pushed new commits. You want to download the latest remote branch info without modifying your working branch. Which command, and how is it different from git pull? [4]**

**Answer:**
- `git fetch origin` - downloads remote commits into remote-tracking refs (`origin/main`) but does **not** touch your working files or branch.
- `git pull` = **`git fetch` + `git merge`** - it downloads *and* merges into your current branch, which can change your working files.
- Use `fetch` when you only want to inspect remote changes before integrating.

**Q6) After fetching the latest changes, update your local main with the latest remote (clean working dir). Which Git command? [4]**

**Answer:** `git pull origin main` (fetch + merge in one). Alternatively `git fetch origin` then `git merge origin/main`.

**Q7) Update the product-search branch with the latest main changes while maintaining a cleaner, linear history. Which command? [4]**

**Answer:** `git rebase main` (while on `product-search`) - replays your feature commits on top of the latest `main`, producing a linear history without a merge commit.

**Q8) Integrate the product-search feature into main. What commands? [4]**

**Answer:**
- `git checkout main` -> `git merge product-search`
- (resolve conflicts if any: edit, `git add`, `git commit`)
- `git push origin main`

**Q9) Configure SSH authentication so developers don't enter username/password repeatedly. Generate an SSH key, add the public key to GitHub and verify the connection. [5]**

**Answer:**
1. **Generate the key:** `ssh-keygen -t rsa -b 4096 -C "you@example.com"` (press Enter to accept `~/.ssh/id_rsa`; optionally add a passphrase).
2. **Copy the public key:** `cat ~/.ssh/id_rsa.pub` (copy the whole line).
3. **Add to GitHub:** GitHub -> **Settings -> SSH and GPG keys -> New SSH key** -> paste -> **Add SSH key**.
4. **Verify the connection:** `ssh -T git@github.com` -> "Hi <username>! You've successfully authenticated...".
5. **Use SSH for the repo:** `git remote set-url origin git@github.com:<user>/<repo>.git`; thereafter push/pull needs no password.

**Q10) You don't have permission to push to the organization's repo. You want to create your own copy, make changes, and contribute them back. Explain the workflow. [5]**

**Answer:**
1. **Fork** the repository on GitHub (creates a personal copy under your account).
2. **Clone** your fork: `git clone <your-fork-url>`.
3. **Add upstream:** `git remote add upstream <original-repo-url>` (to sync later).
4. Create a feature branch, make changes, commit, push to your fork: `git push -u origin <branch>`.
5. Open a **Pull Request** from your fork/branch to the original repository; the owner reviews and merges it.
6. (Keep your fork updated: `git fetch upstream` -> `git rebase upstream/main`.)

### Part III - Containerization using Docker (20)

**Q1) Write a Dockerfile to build a Docker image for the Online Boutique Store System. [4]**

**Answer:**
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/online-boutique-store.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```
- `FROM` - base image with JDK 17; `WORKDIR` - `/app` working directory; `COPY` - copy the built JAR; `EXPOSE 8080` - document the port; `CMD` - start the application.

**Q2) Build the Docker image with tag name OBS, run the container, and verify that the application works successfully. [4]**

**Answer:**
1. `docker build -t obs:latest .` - build with tag `obs:latest`.
2. `docker run -d -p 8080:8080 --name obs obs:latest` - run detached, map host 8080 to container 8080.
3. Verify: `docker ps` (status Up) and open `http://localhost:8080` in a browser.

**Q3) You need to verify whether online-boutique-store.jar exists inside the container. The container is running. Which command opens a shell inside it? [2]**

**Answer:** `docker exec -it obs /bin/sh` -> then run `ls` (and `pwd`) to check `/app/app.jar`.

**Q4) You modified the app and generated a new JAR. The existing container runs the old version. Stop and remove the old container and create a new one with the updated image. Write the sequence of commands. [3]**

**Answer:**
1. `docker build -t obs:latest .` - rebuild the image with the new JAR.
2. `docker stop obs` - stop the old container.
3. `docker rm obs` - remove it.
4. `docker run -d -p 8080:8080 --name obs obs:latest` - create and run the updated container.

**Q5) Pull the Nginx image and run it, exposing nginx to port 8081. [3]**

**Answer:**
- `docker pull nginx` - download the official Nginx image.
- `docker run -d -p 8081:80 --name nginx-app nginx` - Nginx listens on port **80** internally, so map host **8081 -> 80**; access `http://localhost:8081`.

**Q6) You're not sure which container is using port 8081. How do you check? [1]**

**Answer:** `docker ps` (inspect the PORTS column) or `docker port <container>` or `docker ps --filter "publish=8081"`.

**Q7) Explain the steps required to tag and push the OBS image to Docker Hub. [3]**

**Answer:**
1. `docker tag obs:latest <username>/obs:latest` - add your Docker Hub namespace.
2. `docker login` - authenticate.
3. `docker push <username>/obs:latest` - upload.
4. Verify on `hub.docker.com` (your repository page).

---

## B6. SET-8 - Vehicle Rental Management System (CSE-B)

> **Section:** CSE-B - **Faculty:** M Nikitha - **Paper:** SET-8 (Vehicle Rental)

**Repo:** `https://github.com/nikithamoturi/VehicleRentalManagementSystem.git` - **the paper is structurally identical to B2 (SET-4).** Use all B2 answers, substituting the names below:

| SET-4 (Online Shopping) item | SET-8 (Vehicle Rental) replacement |
|---|---|
| `OnlineShoppingApp.git` | `VehicleRentalManagementSystem.git` |
| `products.jsp` | `vehicle.jsp` |
| Product Category / Quantity (Q3c) | Vehicle Type / Availability Status |
| Rental Rate (Q4a) | (add Rental Rate field) |
| Branch `feature/product-update` | Branch `feature/vehicle-update` |
| Image `onlineshopping:1.0` | Image `vehiclerentalapp` |
| Container `online-shopping` | Container `vehicle-rental` |
| `OnlineShopping.war` | `VehicleRental.war` |

Everything else (Maven Q1-Q2, Git Q3-Q4, Docker Q5-Q6, all commands) is exactly the same as **B2 (SET-4)**.

---

## B7. SET-3 - Online Recruitment System (CSE-A)

> **Section:** CSE-A - **Faculty:** K Yasaswini - **Paper:** SET-3 (Online Recruitment) - **Repo:** `https://github.com/ssvkotamraju/ORS.git`

### Part I - Maven (40)

**Q) What steps would you follow to clone the repository, import it correctly into Eclipse, and verify that the pom.xml file is recognized?**
1. `git clone https://github.com/ssvkotamraju/ORS.git` then `cd ORS`.
2. Eclipse: **File -> Import -> Maven -> Existing Maven Projects -> Browse** to the folder -> tick `pom.xml` -> **Finish**.
3. Verify: the project shows the Maven "M" icon; `pom.xml` opens without errors; right-click -> **Maven -> Update Project** resolves dependencies; `mvn validate` gives BUILD SUCCESS.

**Q) How would you identify the problematic dependencies, modify pom.xml, update the Maven project, and verify that the project builds successfully?**
1. Read the error in the console/Problems view to find the failing dependency.
2. Check its `groupId`/`artifactId`/`version` against `mvnrepository.com`; correct typos/versions in `<dependencies>`.
3. Right-click project -> **Maven -> Update Project** to refresh.
4. `mvn clean install` (or `mvn dependency:resolve`) and confirm **BUILD SUCCESS**; `mvn dependency:tree` to confirm it resolves.

**Q) How would you identify the dependency conflict and modify pom.xml to use a compatible version?**
1. `mvn dependency:tree` shows two versions of the same library (Maven already picked the nearest one).
2. Decide the compatible version, then pin it in `<dependencyManagement>` (or add an `<exclusion>` for the unwanted transitive version).
3. Rebuild `mvn clean package` and re-check the tree - only the chosen version should remain.

**Q) What changes would you make in pom.xml and Eclipse to resolve the Java version compatibility issue and successfully execute the project?**
1. In `pom.xml`, set `<maven.compiler.source>`/`<maven.compiler.target>` (or the `maven-compiler-plugin` `<source>`/`<target>`) to the installed JDK, e.g. 17.
2. In Eclipse: right-click project -> **Properties -> Java Build Path -> Libraries** set the correct JRE, then **Maven -> Update Project** (tick "Force Update").
3. Rebuild `mvn clean compile` and run.

**Q) Explain the steps you would follow to troubleshoot the issue, clean the project, refresh Maven dependencies, and confirm a successful build.**
1. Read the error to localise the cause.
2. `mvn clean` (delete stale output), then **Maven -> Update Project** in Eclipse (Force Update) to refresh dependencies.
3. `mvn clean install` (or `-X` for debug) and confirm **BUILD SUCCESS**.

**Q) How would you diagnose the problem and configure the required server/port settings so that the Online Recruitment System can be accessed through a browser?**
1. Check Tomcat is running and the WAR is deployed in `webapps`; view logs (`catalina.out`) for deployment errors.
2. In Eclipse Servers view, double-click Tomcat to open its config and set the HTTP port.
3. Use the correct URL `http://localhost:<port>/<context>/`.

**Q) How would you identify the application using port 8080 and configure the ORS application to run on another available port?**
1. Identify: `netstat -ano | findstr :8080` (Windows) / `lsof -i :8080` (Linux) to find the PID, or check the Servers view.
2. In Eclipse Servers view, change Tomcat's HTTP/1.1 connector port (e.g. to 8081), save, restart.
3. Access `http://localhost:8081/ORS/`.

**Q) How would you identify the Maven compiler configuration causing the problem and modify the pom.xml to use a Java version supported by your installed JDK?**
1. Locate `<properties>` (`maven.compiler.source/target`) or the `maven-compiler-plugin` `<configuration>` in `pom.xml`.
2. Change `<source>`/`<target>` to the installed JDK version (e.g. 17).
3. Rebuild `mvn clean compile`.

**Q) How would you determine whether the problem is caused by an incorrect dependency declaration, repository configuration, network connectivity, or Maven's local cache?**
1. **Declaration:** `mvn dependency:tree` / verify coordinates.
2. **Repository:** check `<repositories>` in `pom.xml` and `<mirrors>` in `settings.xml`.
3. **Network:** `mvn -X` shows download attempts/errors; test connectivity/proxy.
4. **Local cache:** check `~/.m2/repository/...` for a corrupted/partial JAR (delete the folder to force re-download).

**Q) What Maven commands and configuration checks would you perform to identify differences in the JDK, Maven version, local repository, and project dependencies?**
- `java -version`, `mvn -version` (JDK + Maven versions)
- `mvn help:effective-settings` / check `settings.xml` (local repository path)
- `mvn dependency:tree` (project dependencies) and check `~/.m2/repository`

### Part II - Git & GitHub (40)

**Q) How would you clone the GitHub repository, create a working branch, and verify that your local repository is correctly connected to the remote repository?**
- `git clone <url>` -> `cd ORS`
- `git checkout -b feature/apply-fix`
- Verify: `git remote -v`, `git branch -a`.

**Q) Before pushing your changes, how would you retrieve the latest remote changes and determine whether your branch is behind the remote branch?**
- `git fetch origin` then compare: `git status` (says "behind by N commits") or `git log HEAD..origin/main --oneline`.

**Q) What Git commands would you use to update your local branch and rebase your changes onto the latest remote branch?**
- `git fetch origin` -> `git rebase origin/main` (or `git pull --rebase origin main`).

**Q) How would you identify the conflict, decide which changes to keep, edit the file, stage it, and continue the rebase?**
- `git status` shows the conflicted file; open it, remove `<<<<<<<`/`=======`/`>>>>>>>` markers, keep the correct code; `git add <file>`; `git rebase --continue`.

**Q) How would you systematically resolve all the conflicts and verify that the rebase completed successfully?**
- Repeat: fix each conflict -> `git add` -> `git rebase --continue` until the rebase finishes; verify with `git status` ("successfully rebased") and `git log --oneline`.

**Q) How would you investigate the commit history and restore the missing changes without unnecessarily losing your own work?**
- `git log --oneline --graph --all` and `git reflog` to locate the commit where the change existed; `git cherry-pick <hash>` or `git checkout <hash> -- <file>` to restore it, or `git revert` a removal.

**Q) How would you cancel the rebase safely and return your branch to its previous state?**
- `git rebase --abort`.

**Q) What steps would you take to configure an SSH key, add the public key to GitHub, test the SSH connection, and retry the push?**
1. `ssh-keygen -t rsa -b 4096 -C "you@example.com"` (accept default `~/.ssh/id_rsa`).
2. `cat ~/.ssh/id_rsa.pub` and add it in GitHub **Settings -> SSH and GPG keys -> New SSH key**.
3. Test: `ssh -T git@github.com` ("successfully authenticated").
4. Set the remote to SSH (`git remote set-url origin git@github.com:...`) and `git push`.

**Q) How would you verify that the correct version of apply.jsp is present on GitHub and that your commits contain only the intended changes?**
- On GitHub, open `apply.jsp` and its history/commits; locally run `git show <hash>` / `git log -p -- apply.jsp` and `git diff origin/main` to confirm only intended changes are present.

**Q) What type of push would be appropriate after a rebase, and what precautions should you take before using it on a shared branch?**
- After rebasing you rewrite history, so a normal push is rejected -> you need a **force push**, preferably **`git push --force-with-lease`** (safer: only overwrites if no one else pushed).
- **Precaution:** never force-push a shared branch others have pulled; warn the team first, or use revert/merge instead.

### Part III - Docker (20)

**Tasks:** Dockerfile -> build image `ORS` -> push to Docker Hub; run container exposing 8080; check `http://localhost:8080`.
```dockerfile
FROM tomcat:9-jdk17
COPY target/ORS.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- `mvn clean package` -> `docker build -t ors:latest .` -> `docker tag ors:latest <user>/ors:latest` -> `docker login` -> `docker push <user>/ors:latest`
- `docker run -d -p 8080:8080 --name ors ors:latest`; open `http://localhost:8080/ORS/`.

**Qa) What information would you need before creating the Dockerfile, and what major instructions would you include to build a Docker image capable of running the ORS application?**
- Need: base image (Tomcat/JDK), the built artifact (WAR/JAR), its path, the app port, and the start command.
- Include: `FROM`, `WORKDIR`, `COPY` (source + WAR), `RUN` (if building), `EXPOSE 8080`, `CMD`/`ENTRYPOINT`.

**Qb) How would you troubleshoot the Dockerfile, project structure, build artifact, and Docker build context?**
- Check Dockerfile syntax/instruction names; ensure `.` is the project root and `COPY` sources exist (`target/ORS.war`); confirm the base image is pullable; read the build error line and fix.

**Qc) How would you run the container so that container port 8080 is correctly mapped to host port 8080?**
- `docker run -d -p 8080:8080 --name ors ors:latest` (format `-p HOST:CONTAINER`).

**Qd) What changes could you make to the Dockerfile and Docker build process to reduce the image size and improve build efficiency?**
- Use a **multi-stage build** (build stage with Maven, runtime stage with only Tomcat/JRE).
- Use a slim/alpine base image; `COPY` only the WAR (not the whole project); combine `RUN` commands; order layers from least- to most-frequently changed to maximise cache; add a `.dockerignore` (exclude `target`, `.git`).

**Qe) Explain how you would tag the image appropriately, authenticate with Docker Hub, push the image, and verify that it is available in the repository.**
- `docker tag ors:latest <username>/ors:latest` -> `docker login` -> `docker push <username>/ors:latest` -> verify on `hub.docker.com`.

---

## B8. Set-2 (2) - Car Booking System (CSE-G)

> **Section:** CSE-G - **Faculty:** Anuj - **Paper:** Set-2 (2) (Car Booking) - **Repo:** `https://github.com/anujyog1/carrepo.git`
> **Main task:** clone, resolve dependencies via `pom.xml`, build the WAR/JAR, verify the artifact in `target/`.

### Part I - Maven Scenario Questions

**Q1) A teammate sends a .patch file for a bug fix. How would you apply it and include it in your Maven build?**
- `git apply bug-fix.patch` (or `git am bug-fix.patch`) to apply it; then build with `mvn clean package` so the patch is included in the artifact.

**Q2) Change the default build output directory from target/ to build_output/. How would you configure it?**
- In `pom.xml`:
  ```xml
  <build>
    <directory>build_output</directory>
  </build>
  ```

**Q3) How does Maven resolve dependency conflicts when two libraries use different versions of the same dependency, and how can you view and manage the dependency tree?**
- Maven uses **nearest-wins** mediation (closest to root; tie -> first declared). View with `mvn dependency:tree`; manage by pinning versions in `<dependencyManagement>` or excluding via `<exclusions>`.

**Q4) What command do you use to build a WAR file in Maven, where is it generated, and how can you deploy it to a server like Apache Tomcat?**
- `mvn package`; generated in `target/` (`<finalName>.war` or `artifactId-version.war`). Deploy by copying it into Tomcat's `webapps/` (or **Run on Server** in Eclipse) and accessing `http://localhost:8080/<context>/`.

**Q5) How can you create an executable JAR with a main method using Maven, and which plugin helps configure this behavior?**
- Use `maven-jar-plugin` with `<archive><manifest><mainClass>...` (or `maven-assembly`/`shade` for a fat JAR); `mvn clean package`; run with `java -jar target/app.jar`.

**Q6) You need to build the carrepo JAR quickly for a local demo, but tests take too long. What flag do you append to mvn package to compile and package while skipping test execution?**
- `-DskipTests` (e.g. `mvn clean package -DskipTests`); `-Dmaven.test.skip=true` skips compiling tests too.

**Q7) You want the full list of all direct and transitive dependencies Maven resolved. What simple Maven command prints the entire dependency tree?**
- `mvn dependency:tree`.

**Q8) You use Java 17 in multiple places inside pom.xml; you want to define it once centrally. How?**
- Declare a property and reference it:
  ```xml
  <properties>
    <java.version>17</java.version>
  </properties>
  <maven.compiler.source>${java.version}</maven.compiler.source>
  <maven.compiler.target>${java.version}</maven.compiler.target>
  ```

**Q9) carrepo is deployed onto an external Tomcat that already includes Servlet API libraries. You want Maven to use the Servlet API for local compilation but not package it into the WAR. Which <scope> should you set?**
- `<scope>provided</scope>`.

**Q10) You need to know where Maven stores downloaded JAR files by default, and how to clear them if corrupted.**
- Default: `~/.m2/repository` (`C:\Users\<user>\.m2\repository`). Delete the specific artifact's folder (or the whole repository) to force re-download.

### Part II - Git & GitHub

**Tasks:** Initialize a Git repository and add the Maven project files; set global config and push to GitHub.
- `git init` -> `git add .` -> `git commit -m "Initial commit"`; `git config --global user.name/email`; create repo; `git remote add origin <url>`; `git push -u origin main`.

**Q) How do you set up a new local branch feature/engine-update that tracks a new remote branch of the same name, and push your initial commit to GitHub? [4]**
- `git checkout -b feature/engine-update` -> make changes -> `git add .` -> `git commit -m "..."` -> `git push -u origin feature/engine-update` (`-u` sets tracking).

**Q) You are editing CarController.java with incomplete code; a critical bug needs a fix on main. How do you temporarily save your work, switch to main, apply a hotfix, and return? [6]**
- `git stash` -> `git checkout main` -> fix bug -> `git add`/`git commit` -> `git checkout feature/...` -> `git stash pop`.

**Q1) How do you include the forgotten file and fix the commit message without creating a second cluttering commit?**
- `git add <forgotten-file>` -> `git commit --amend -m "Corrected message"` (only if not pushed).

**Q2) How do you move your uncommitted changes over to feature-login without losing anything or dirtying main?**
- `git stash` -> `git checkout -b feature-login` (or switch to it) -> `git stash pop`.

**Q3) You and a teammate edited the same line in login.jsp; git merge feature-user reports a conflict. How do you resolve it?**
- `git status` -> open `login.jsp`, remove the `<<<<<<<`/`=======`/`>>>>>>>` markers keeping the desired code -> `git add login.jsp` -> `git commit`.

**Q4) You modified app.js but it broke everything; discard the changes and reset the file to the last commit.**
- `git restore app.js` (or `git checkout -- app.js`).

**Q5) You accidentally ran git add secret.env; you don't want to commit it. How do you unstage it?**
- `git restore --staged secret.env` (or `git reset HEAD secret.env`).

**Q6) You forgot which lines you added/modified before staging. How do you check?**
- `git diff` (unstaged changes, line by line).

**Q7) You want to switch from a feature branch to main but aren't sure which branch you're on. How do you check and go to main?**
- `git branch` (current marked `*`) or `git status` -> `git checkout main`.

**Q8) You want to quickly check the last 4 commits without clutter. Which command?**
- `git log -4 --oneline`.

**Q9) Your teammate pushed updates to remote main; get them onto your local machine, apply your changes, and push back.**
- `git pull origin main` (or `git fetch` + `git merge`/`git rebase`) -> make your changes -> `git add .` -> `git commit -m "..."` -> `git push origin main`.

**Q10) You finished merging bugfix into main; delete the local bugfix branch, and force-delete it.**
- `git branch -d bugfix` (safe) / `git branch -D bugfix` (force).

### Part III - Docker

**Tasks:** Dockerfile (copy WAR/JAR, run on Tomcat); build image and run; tag and push to Docker Hub.
```dockerfile
FROM tomcat:9-jdk17
COPY target/carrepo.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
- `docker build -t carrepo:latest .` -> `docker run -d -p 8080:8080 --name carrepo carrepo:latest` -> `docker tag`/`login`/`push`.

**Q1) Which two Docker commands let you (1) inspect stdout logs and (2) open an interactive terminal inside the running container?**
- `docker logs <container>` and `docker exec -it <container> /bin/sh`.

**Q2) What single safety-checked Docker command clears out all stopped containers, unused networks, and dangling images at once?**
- `docker system prune` (add `-a` for all unused images).

**Q3) How do you create and start a container named my-redis from the redis image?**
- `docker run --name my-redis -d redis`.

**Q4) How do you open the Redis command-line tool inside the container and come out of it?**
- `docker exec -it my-redis redis-cli` -> `exit`.

**Q5) Your application is running inside Docker, but you're not sure if the container is active. Which command checks running containers?**
- `docker ps`.

**Q6) You want to run your car_app container and expose its internal port 5000 on host port 8080. Which command?**
- `docker run -d -p 8080:5000 --name car_app car_app`.

**Q7) You built a car_app image but forgot to tag it. How do you tag it now?**
- `docker tag <image-id> car_app:latest` (or `docker tag <image-id> <username>/car_app:latest`).

**Q8) Your car_app container is running but you want to debug it with a shell; also how do you control/limit RAM in Docker?**
- Shell: `docker exec -it car_app /bin/sh`.
- Limit RAM: `docker run -d --memory="512m" --name car_app car_app` (optionally `--memory-swap`).

---

## B9. Set-3 (2) - Train Booking System (CSE-G)

> **Section:** CSE-G - **Faculty:** Anuj - **Paper:** Set-3 (2) (Train Booking) - **Repo:** `https://github.com/anujyog1/trainrepo.git`
> **Main task:** clone, resolve dependencies via `pom.xml`, build the WAR/JAR, verify the artifact in `target/`.

### Part I - Maven Scenario Questions

**Q1) You have multiple JUnit test failures and want to rerun only the failed tests. How would you approach this?**
- Read the failed test names from `target/surefire-reports/`, then rerun each with `mvn -Dtest=<FailedTest> test`; or use `-Dsurefire.rerunFailingTestsCount=1`.

**Q2) You want to skip tests during the Maven build. What command would you use?**
- `mvn package -DskipTests` (or `-Dmaven.test.skip=true`).

**Q3) How would you generate a site report (with test coverage, dependency analysis) for a Maven project?**
- `mvn site` (add reporting plugins like `maven-surefire-report-plugin`/JaCoCo for coverage); the report is generated in `target/site/`.

**Q4) How do you write and run a JUnit test, and where are the compiled test classes and reports stored after mvn test?**
- Put tests in `src/test/java` with `@Test` methods; run `mvn test`. Compiled test classes: `target/test-classes/`; reports: `target/surefire-reports/`.

**Q5) How do you install and use a custom third-party JAR and confirm it's included in the build and classpath?**
- `mvn install:install-file -Dfile=lib.jar -DgroupId=... -DartifactId=... -Dversion=... -Dpackaging=jar`; declare it as a `<dependency>`; confirm with `mvn dependency:tree`.

**Q6) You just cloned trainrepo. What is the very first basic Maven command to compile the source and run unit tests?**
- `mvn test` (compiles main + tests and runs tests); `mvn compile` only compiles main.

**Q7) You want to clean up all generated build artifacts so the next build starts fresh. Which command?**
- `mvn clean`.

**Q8) You want to package the code into a deployable .jar/.war and install it locally so other local projects can use it. Which command?**
- `mvn clean install`.

**Q9) A build is failing due to a missing dependency. Where in the project structure do you look to add/check declared dependencies?**
- In `pom.xml` (the `<dependencies>` section).

**Q10) After a build, where does Maven physically store the generated output/packaged artifact?**
- In the `target/` directory.

### Part II - Git & GitHub

**Q1) How do you pause work on your feature branch without committing, switch to main, create a hotfix, merge it back, and resume?**
- `git stash` -> `git checkout main` -> create hotfix (branch or direct), commit, `git merge` -> `git checkout feature` -> `git stash pop`.

**Q2) Two developers update routes.json simultaneously (arrival vs departure); Git flags a conflict. How do you resolve it preserving both?**
- `git status` -> open `routes.json`, remove markers, keep **both** the arrival and departure changes -> `git add routes.json` -> `git commit`.

**Q3) Another developer pushed updates to remote main; fetch and merge them before starting work, then work and push.**
- `git fetch origin` -> `git merge origin/main` (or `git pull origin main`) -> work -> `git add`/`git commit` -> `git push origin main`.

**Q4) (Same as Q3.)** Use the same fetch/merge/work/push sequence.

**Q5) You updated train_station_codes.csv and committed; remote main has 2 new commits. Keep a clean history (no merge commit) by rebasing, then push.**
- `git pull --rebase origin main` (or `git fetch origin` + `git rebase origin/main`) -> `git push origin main`.

**Q6) You committed a new feature but forgot booking_controller.js. How do you include the file in your commit?**
- `git add booking_controller.js` -> `git commit --amend --no-edit`.

**Q7) You edited train_schedules.json by mistake; discard changes and revert the file to the last commit.**
- `git restore train_schedules.json`.

**Q8) You wrote code for a new feature on main by mistake (not committed); move these changes to a new branch feature-train-search.**
- `git checkout -b feature-train-search` (uncommitted changes carry over to the new branch) -> `git add .` -> `git commit -m "..."`.

**Q9) Concise single-line log of the last 5 commits.**
- `git log -5 --oneline`.

**Q10) Download all updates, branches, and tags from the remote without modifying or auto-merging any files.**
- `git fetch --all --tags` (or `git fetch origin`).

**Q11) Write the git command to use another developer's project which is not publicly available.**
- `git clone <private-repo-URL>` (with authentication - SSH key or username/PAT for HTTPS).

### Part III - Docker

**Tasks:** Dockerfile (copy WAR/JAR, run on Tomcat); build image and run; tag and push to Docker Hub.
```dockerfile
FROM tomcat:9-jdk17
COPY target/trainrepo.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

**Q1) Which two Docker CLI commands help diagnose why a container crashed immediately after starting?**
- `docker ps -a` (check exit code) and `docker logs <container>` (error output).

**Q2) You want to test a bash command in an Ubuntu container without leaving a stopped container on disk.**
- `docker run --rm -it ubuntu /bin/bash` (`--rm` auto-removes the container on exit).

**Q3) How do you view the error logs from the stopped container?**
- `docker logs <container>`.

**Q4) Map host port 80 to Tomcat's internal port 8082 when starting train-app.**
- `docker run -d -p 80:8082 --name train-app train-app:latest`.

**Q5) You want to start a container and let it run in the background. Which command?**
- `docker run -d ...`.

**Q6) You're not sure which container is using port 3000. How do you check?**
- `docker ps` (PORTS column) or `docker port <container>` or `docker ps --filter "publish=3000"`.

**Q7) You built an image but forgot to tag it. How do you tag it now?**
- `docker tag <image-id> <name>:<tag>`.

**Q8) You updated server.js, but docker run my-api still runs the old code. What do you run to get the updated build?**
- Rebuild and recreate: `docker build -t my-api:latest .` -> `docker stop my-api` -> `docker rm my-api` -> `docker run -d my-api:latest`.

---

## B10. Set-5 (1) - Online Vehicle Rental, OVR (Haleema)

> **Section:** CSE (branch not stated in the paper) - **Faculty:** Haleema - **Paper:** Set-5 (1) (Online Vehicle Rental) - **Repo:** `https://github.com/haleema91/Internal-1-OVR.git`

### Part I - Maven

**Q1) Clone the project from GitHub. [4]**
- `git clone https://github.com/haleema91/Internal-1-OVR.git` -> `cd Internal-1-OVR` -> `ls` to verify `pom.xml`.

**Q2) Identify all the errors in the pom.xml. [6]**
- Check for: wrong/missing `<packaging>` (needs `war` or `jar` as intended); incorrect dependency coordinates/versions; compiler `source`/`target` set to an unsupported old Java; plugin missing `<groupId>`; XML typos (`<artificatId>`); JUnit dependency without `<version>`. Fix each and rebuild.

**Q3) Build and run the Maven project. [5]**
- `mvn clean compile` -> `mvn test` -> `mvn package`; verify `target/*.war|jar`; for a web app deploy the WAR to Tomcat (Run on Server) and open it in the browser.

**Q4) The application is packaged as a WAR, but the company wants a standalone JAR. What changes in pom.xml? [5]**
- Change `<packaging>war</packaging>` -> `<packaging>jar</packaging>`; remove web-only dependencies; optionally add `maven-jar-plugin` with `<mainClass>`; `mvn clean package`; run `java -jar target/<name>.jar`.

**Q5) Add the PostgreSQL JDBC driver dependency. How will you add it to pom.xml? [4]**
```xml
<dependency>
  <groupId>org.postgresql</groupId>
  <artifactId>postgresql</artifactId>
  <version>42.7.3</version>
</dependency>
```
- Maven downloads it on the next build (`mvn clean install`).

**Q6) The testing phase fails because the project contains a JUnit dependency with no <version>. How do you fix it? [3]**
- Add an explicit `<version>` (e.g. `junit-jupiter 5.10.0` with `<scope>test</scope>`).

**Q7) You want to skip tests during the Maven build. What command? [2]**
- `mvn package -DskipTests`.

**Q8) How do you build a Java project with Maven, and what files are generated in target/ after mvn clean install? [3]**
- `mvn clean install`. In `target/`: `classes/` (compiled `.class`), `test-classes/`, `surefire-reports/`, and the final `jar`/`war`; the artifact is also installed to `~/.m2/repository`.

**Q9) Your Maven build fails due to "Unsupported class version error." What plugin and configuration would you review? [3]**
- Review the `maven-compiler-plugin` (or `maven.compiler.source`/`target` properties) and set `<source>`/`<target>` to match the installed JDK.

**Q10) Push the Maven project to GitHub. [5]**
- `git init` -> `git add .` -> `git commit -m "Initial commit"` -> `git remote add origin <url>` -> `git push -u origin main`.

### Part II - Git & GitHub

**Q1) Initialize the project as a Git repository. [3]** - `git init`
**Q2) Configure Git with username rentaldev and email dev@rental.com. [2]**
- `git config user.name "rentaldev"` and `git config user.email "dev@rental.com"` (add `--global` for all repos).
**Q3) You created VehicleService.java and want to stage it. [2]** - `git add VehicleService.java`
**Q4) Commit the staged changes with the message "Added Vehicle Management Module". [3]** - `git commit -m "Added Vehicle Management Module"`
**Q5) See the differences in VehicleController.java before committing. [3]** - `git diff VehicleController.java`
**Q6) Display the complete commit history. [3]** - `git log`
**Q7) You accidentally staged application.properties containing credentials. Unstage it. [3]** - `git restore --staged application.properties`
**Q8) You modified RentalService.java and want to discard the changes. [3]** - `git restore RentalService.java`
**Q9) Create a new branch vehicle-booking. [3]** - `git checkout -b vehicle-booking`
**Q10) Your vehicle-booking branch is behind main; apply your commits on top of the latest main. [4]** - `git rebase main`
**Q11) Your payment branch is behind main by 3 commits; get the latest changes. [5]** - `git pull origin main` (or `git fetch origin` + `git rebase origin/main`)
**Q12) You are on the payment branch and need to switch back to main. [4]** - `git checkout main`

### Part III - Docker

**Q1) Write a Dockerfile for the Online Vehicle Rental System. [4]**
```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/ovr.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```
**Q2) Build the image with tag name OVR, run the container, and verify OVR works. [4]**
- `docker build -t ovr:latest .` -> `docker run -d -p 8080:8080 --name ovr ovr:latest` -> `docker ps`; open `http://localhost:8080`.
**Q3) Verify which containers are currently active. [2]** - `docker ps`
**Q4) An OVR container is consuming high CPU; how do you stop it? [2]** - `docker stop <container>`
**Q5) The OVR application crashed. Which command views its logs? [2]** - `docker logs <container>`
**Q6) After building the OVR image, verify it was created and view all images. [2]** - `docker images`
**Q7) Tag and push the OVR image to Docker Hub. [4]**
- `docker tag ovr:latest <username>/ovr:latest` -> `docker login` -> `docker push <username>/ovr:latest`.

---

## B11. Set-6 (1) - Online Event Management, OEMS (Haleema)

> **Section:** CSE (branch not stated in the paper) - **Faculty:** Haleema - **Paper:** Set-6 (1) (Online Event Management) - **Repo:** `https://github.com/haleema91/Internal-1-OEMS.git`

### Part I - Maven (Java Web Application)

**Q1) Clone the OEMS Maven Web Application. [4]** - `git clone https://github.com/haleema91/Internal-1-OEMS.git` -> `cd Internal-1-OEMS`.
**Q2) Identify all errors in pom.xml that prevent the web app from building. [6]**
- Wrong `<packaging>` (must be `war` for Tomcat); bad dependency coordinates/versions; compiler version pointing to an old Java; missing plugin `<groupId>`; missing Servlet/JSTL dependencies; XML typos. Fix and rebuild.
**Q3) Build the web application and generate the WAR. Which command, and how verify? [5]**
- `mvn clean package`; verify `target/*.war` exists (`ls target/` or `jar tf target/<name>.war`).
**Q4) The pom.xml has <packaging>jar</packaging> but it should run on Tomcat. What should packaging be? Write the config. [5]**
- `<packaging>war</packaging>` inside `<project>`.
**Q5) How will you add the Servlet API and JSTL dependencies? [4]**
```xml
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
  <version>4.0.1</version>
  <scope>provided</scope>
</dependency>
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>jstl</artifactId>
  <version>1.2</version>
</dependency>
```
**Q6) The project was built with an older Java, but your system uses a newer JDK. What causes the error and how do you configure the Maven Compiler Plugin? [3]**
- "Source/Target option no longer supported" occurs because the compiler `source`/`target` is an old Java version. Configure the `maven-compiler-plugin` `<source>`/`<target>` (or `maven.compiler.source/target`) to the installed JDK (e.g. 17).
**Q7) Tomcat reports port 8080 already in use. How do you identify the process and resolve it? [3]**
- Identify: `netstat -ano | findstr :8080` (Windows) / `lsof -i :8080` (Linux). Resolve by stopping the other process or changing Tomcat's HTTP port in the server configuration.
**Q8) Maven produces unexpected compilation results; old .class files may be in target. Which command removes old artifacts and does a fresh build? [2]**
- `mvn clean package`.
**Q9) The project was developed using Java 17 but the system has Java 21. How do you configure Maven to compile using Java 17? [3]**
- Set the compiler plugin (or `maven.compiler.source/target` properties) to 17; optionally install JDK 17 or configure the Maven Toolchains plugin.
**Q10) Push the complete Maven web application project to GitHub. Write the commands. [5]**
- `git init` -> `git add .` -> `git commit -m "Initial commit"` -> `git remote add origin <url>` -> `git push -u origin main`.

### Part II - Git & GitHub

**Q1) The project is not tracked by Git. How do you start tracking it and make the first commit? [3M]**
- `git init` -> `git add .` -> `git commit -m "Initial commit"`.
**Q2) You modified Event.java and created Registration.java. How do you check what changed and what files Git detects? [3M]**
- `git status` (modified/new files) and `git diff` (line changes).
**Q3) How would you create and work on a separate registration branch? [4M]**
- `git checkout -b registration` -> work -> `git add`/`git commit`.
**Q4) The feature is complete on the registration branch; integrate it into main. [4M]**
- `git checkout main` -> `git merge registration` -> (resolve conflicts) -> `git push origin main`.
**Q5) While merging registration into main, Git reports a conflict in Registration.java. How do you handle it? [5M]**
- `git status` -> open `Registration.java`, remove the `<<<<<<<`/`=======`/`>>>>>>>` markers keeping the desired code -> `git add Registration.java` -> `git commit`.
**Q6) You changed Event.java but don't want to commit; send the changes as a .patch file. How do you create and share it? [3M]**
- `git diff > event.patch` (or commit then `git format-patch -1 HEAD` to include the commit/message); share the `.patch` file.
**Q7) A teammate sends a .patch file for Booking.java. How do you apply it without manual copying? [3M]**
- `git apply booking.patch` (or `git am booking.patch` if it was made with `format-patch`).
**Q8) You accidentally committed a buggy validation change and already pushed it. Undo it while keeping history intact. [4M]**
- `git revert <commit-hash>` -> `git push origin main`.
**Q9) You modified EventServlet.java but want to discard the changes (not committed). [2M]**
- `git restore EventServlet.java` (or `git checkout -- EventServlet.java`).
**Q10) You accidentally staged Registration.java but want to keep the modifications. Unstage it. [2M]**
- `git restore --staged Registration.java` (or `git reset HEAD Registration.java`).
**Q11) You're on the registration branch and a teammate pushed 3 new commits to main; get the latest changes. [4M]**
- `git pull origin main` (or `git fetch origin` + `git rebase origin/main`).
**Q12) You're on the registration branch and need to switch back to main. [2M]**
- `git checkout main`.

### Part III - Docker

**Q1) Write a Dockerfile for the OEMS WAR to be deployed on Apache Tomcat. [4]**
```dockerfile
FROM tomcat:9-jdk17
COPY target/OEMS.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
```
**Q2) Build the image with tag oems-web, run the container, and verify it is accessible on port 7070. [4]**
- `docker build -t oems-web:latest .` -> `docker run -d -p 7070:8080 --name oems oems-web:latest` -> open `http://localhost:7070/OEMS/`.
**Q3) Inspect the Tomcat directory inside the running container to verify OEMS.war was copied; open an interactive shell. [2]**
- `docker exec -it oems /bin/sh` -> `ls /usr/local/tomcat/webapps/` (confirm `OEMS.war`).
**Q4) The OEMS web application is not loading; view the container logs. [2]**
- `docker logs oems` (or `docker logs -f oems`).
**Q5) Start an OEMS container and let it run in the background. [2]**
- `docker run -d --name oems oems-web:latest` (with a port mapping if needed).
**Q6) Pull Ubuntu, run a container, enter it, install git, verify the installation, and run simple git commands. [2]**
- `docker pull ubuntu` -> `docker run -it --name u1 ubuntu /bin/bash` -> `apt-get update && apt-get install -y git` -> `git --version` -> `git config --global user.name "test"` -> `git status`.
**Q7) Tag the OEMS image and push it to Docker Hub. [4]**
- `docker tag oems-web:latest <username>/oems-web:latest` -> `docker login` -> `docker push <username>/oems-web:latest` -> verify on `hub.docker.com`.
