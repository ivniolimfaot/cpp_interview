# SCM/CI/CD

## General Info

### What are the types of SCM?

Source Code Management (SCM), also known as Version Control System (VCS), is a software tool used by software developers to manage changes to source code over time.

The primary purpose of SCM is to keep track of changes made to source code files and coordinate those changes among multiple developers working on the same project. SCM enables developers to collaborate effectively, track revisions, maintain a history of changes, and revert to previous versions if necessary.

Key features of SCM include:

1. **Versioning**: SCM allows developers to keep track of different versions of source code files. Each change or set of changes is recorded as a new version, enabling developers to compare versions, revert to previous versions, or merge changes from different branches.

2. **Collaboration**: SCM facilitates collaboration among developers by providing mechanisms for sharing code changes, resolving conflicts, and coordinating work on shared codebases. Multiple developers can work on the same codebase simultaneously without interfering with each other's changes.

3. **History Tracking**: SCM maintains a detailed history of changes made to source code files, including who made each change, when it was made, and what changes were made. This history can be useful for tracking the evolution of the codebase, understanding why certain changes were made, and identifying the source of bugs or regressions.

4. **Branching and Merging**: SCM allows developers to create branches, which are separate lines of development that diverge from the main codebase. Branches can be used for implementing new features, experimenting with changes, or isolating bug fixes. Once changes in a branch are complete, they can be merged back into the main codebase.

5. **Conflict Resolution**: When multiple developers make conflicting changes to the same codebase, SCM provides mechanisms for resolving conflicts and merging changes together. Developers can review conflicting changes, choose which changes to keep, and manually resolve conflicts if necessary.

Popular SCM tools include Git, Subversion (SVN), Mercurial, and Perforce. Git, in particular, has become widely adopted in recent years due to its distributed nature, speed, and flexibility.

Source Code Management (SCM) systems, also known as Version Control Systems (VCS), are tools used by developers to manage changes to source code over time. There are several types of SCM systems, each with its own features and functionalities. Here are some of the most common types:

1. **Centralized Version Control Systems (CVCS)**:
   * In CVCS, there is a single central repository where all the code is stored.
   * Developers check out code from this central repository to work on it and then check it back in when they are done.
   * Examples include Concurrent Versions System (CVS) and Subversion (SVN).

2. **Distributed Version Control Systems (DVCS)**:
   * In DVCS, every developer has a copy of the entire repository on their local machine.
   * Developers can work independently without needing constant access to a central server.
   * Examples include Git, Mercurial, and Bazaar.

3. **Git**:
   * Git is the most widely used DVCS and is known for its speed, flexibility, and distributed nature.
   * It allows for branching and merging, facilitating collaborative development workflows.
   * Git is highly popular in open-source projects and enterprise software development.

4. **Mercurial**:
   * Mercurial is another DVCS similar to Git, offering distributed version control capabilities.
   * It emphasizes simplicity and ease of use, making it suitable for various types of projects.
   * While not as ubiquitous as Git, Mercurial is still used in some projects and organizations.

5. **Perforce (Helix Core)**:
   * Perforce is a centralized version control system commonly used in enterprise settings, especially for large-scale projects.
   * It offers features like file locking, branching, and advanced versioning capabilities.
   * Perforce is often favored for its performance and scalability, particularly in industries such as game development and automotive engineering.

6. **Microsoft Team Foundation Version Control (TFVC)**:
   * TFVC is a centralized version control system developed by Microsoft and integrated into Azure DevOps Services (formerly Visual Studio Team Services).
   * It provides features like branching, merging, and shelving, and is tightly integrated with other Microsoft development tools.
   * While Git has gained more popularity in recent years, TFVC is still used by teams that prefer a centralized workflow or have existing investments in Microsoft technologies.

Each type of SCM system has its own advantages and use cases, and the choice often depends on factors such as project size, team preferences, collaboration requirements, and existing infrastructure.

### What are version control systems used for?

A version control system (VCS) is a software tool that helps developers manage changes to source code over time. It allows multiple developers to collaborate on a project by tracking changes, facilitating collaboration, and enabling the management of different versions of files.

There are two main types of version control systems:

1. **Centralized Version Control System (CVCS):** In a CVCS, there is a central server that stores all versions of a file and controls access to it. Developers can check out files from the central repository, make changes, and then check them back in. Examples of CVCS include CVS (Concurrent Versions System) and SVN (Subversion).

2. **Distributed Version Control System (DVCS):** In a DVCS, each developer has a complete copy of the repository, including its full history. This allows developers to work independently and make changes without needing constant access to a central server. Examples of DVCS include Git, Mercurial, and Bazaar.

Git, developed by Linus Torvalds in 2005, has become one of the most widely used version control systems due to its speed, flexibility, and robust branching and merging capabilities. It is particularly popular in open-source projects and in the software development industry in general.

Version control systems (VCS) are used for several purposes in software development and other collaborative projects. Some key uses include:

1. **Tracking Changes:** VCS keeps track of changes made to files over time. This includes who made the changes, when they were made, and what exactly was changed. This history allows developers to understand the evolution of the codebase and revert to previous versions if needed.

2. **Collaboration:** VCS enables multiple developers to work on the same codebase simultaneously. It allows them to work on different features or fixes independently and merge their changes together later. This collaborative workflow promotes teamwork and helps avoid conflicts when multiple people are working on the same files.

3. **Backup and Recovery:** VCS acts as a backup system for project files. Since it stores the complete history of changes, even if a file is accidentally deleted or becomes corrupted, it can be recovered from a previous version. This helps safeguard against data loss and ensures the integrity of the project.

4. **Branching and Merging:** VCS allows developers to create branches, which are separate lines of development that diverge from the main codebase. Branches are often used for implementing new features, fixing bugs, or experimenting with changes. Once the changes are tested and reviewed, they can be merged back into the main codebase. This branching and merging functionality facilitates flexible development workflows.

5. **Code Reviews and Collaboration:** VCS platforms often include tools for code review, where developers can review each other's code changes, provide feedback, and suggest improvements. This fosters collaboration and helps maintain code quality by ensuring that changes are reviewed before being integrated into the main codebase.

6. **Auditing and Compliance:** VCS provides a detailed audit trail of all changes made to the project files. This audit trail can be useful for compliance purposes, such as meeting regulatory requirements or tracking changes for legal or security reasons.

Overall, version control systems play a crucial role in modern software development by providing a structured and efficient way to manage code changes, collaborate with team members, and ensure the integrity and reliability of software projects.

### What are the git commands?

Certainly! Git is a powerful version control system that allows you to manage your source code and collaborate with others efficiently. Here are some essential Git commands:

1. `git init`: Initializes a new Git repository in the current directory.
2. `git clone <repository URL>`: Clones an existing Git repository from a remote server to your local machine.
3. `git add <file>`: Adds a file to the staging area, preparing it to be committed.
4. `git commit -m "commit message"`: Commits the changes in the staging area to the local repository with a descriptive message.
5. `git status`: Displays the status of the working directory, including which files are modified, staged, or untracked.
6. `git pull`: Fetches changes from the remote repository and merges them into the current branch.
7. `git push`: Pushes commits from your local repository to the remote repository.
8. `git branch`: Lists all local branches in the repository.
9. `git branch <branch name>`: Creates a new branch with the specified name.
10. `git checkout <branch name>`: Switches to the specified branch.
11. `git merge <branch name>`: Merges the specified branch into the current branch.
12. `git remote -v`: Lists all remote repositories and their URLs.
13. `git log`: Displays a log of commits, showing the commit message, author, date, and commit hash.
14. `git diff`: Shows the differences between the working directory, staging area, and the last commit.

These are just a few of the most commonly used Git commands. There are many more commands and options available, each serving specific purposes in managing your version-controlled projects.

### What are the steps during a change commit?

During a typical change commit in Git, several steps are involved:

1. **Stage Changes:** After making modifications to files in your working directory, you need to stage the changes you want to commit. This involves using the `git add` command to add specific files or directories to the staging area.

```bash
git add <file1> <file2> ...
```

1. **Review Changes:** You can review the changes you've staged using `git diff --staged` or `git diff --cached` to see what will be committed.

```bash
git diff --staged
```

1. **Commit Changes:** Once you're satisfied with the changes you've staged, you commit them to the repository using the `git commit` command. This command opens an editor where you can write a commit message explaining the changes.

```bash
git commit
```

Alternatively, you can provide the commit message directly using the `-m` option.

```bash
git commit -m "Your commit message here"
```

1. **Review Commit History:** After committing your changes, you can review the commit history using `git log` to see the commits you've made.

```bash
git log
```

1. **Push Changes (if working with a remote repository):** If you're working with a remote repository and want to share your changes with others, you'll need to push your commits to the remote repository using `git push`.

```bash
git push <remote> <branch>
```

These are the general steps involved in making and committing changes in Git. Depending on your workflow and specific requirements, you may also perform additional actions, such as branching, merging, rebasing, etc.

### What is the difference between git fetch and git pull?

`git fetch` and `git pull` are both Git commands used to update your local repository with changes from a remote repository. However, they have different functionalities:

1. **git fetch**:
   * When you run `git fetch`, Git will retrieve the latest changes from the remote repository but will not merge them into your local branch.
   * It updates your remote-tracking branches (e.g., `origin/master`) to reflect the changes in the remote repository.
   * It's useful for checking what changes exist on the remote without integrating them into your local branch immediately.

2. **git pull**:
   * `git pull` does two things: it fetches the changes from the remote repository (same as `git fetch`), and then it automatically merges those changes into your current local branch.
   * It's essentially a combination of `git fetch` followed by `git merge`.

In summary, `git fetch` simply retrieves the latest changes from the remote repository and updates your remote-tracking branches, while `git pull` fetches those changes and automatically merges them into your local branch.

### What are the stages of merge conflict resolution?

Resolving merge conflicts typically involves several stages, which may vary slightly depending on the version control system you're using (e.g., Git). Here's a general outline of the stages involved in resolving merge conflicts:

1. **Identifying the Conflict**: The first step is to identify that a conflict exists. This usually happens when you attempt to merge two branches, and the version control system detects conflicting changes between them.

2. **Locating the Conflict**: Once the conflict is identified, you need to locate the files or specific sections within files where the conflict occurs. Your version control system will typically mark these areas in the affected files.

3. **Understanding the Conflict**: Take time to understand why the conflict occurred. This involves reviewing the changes made in both branches and understanding how they conflict with each other. Understanding the nature of the conflict will help in resolving it effectively.

4. **Choosing a Resolution Strategy**:
   * **Manual Resolution**: Manually edit the conflicting files to incorporate the desired changes from both branches. This can involve carefully reviewing each conflicting section and deciding how to combine or modify the changes to achieve the desired outcome.
   * **Accepting Changes from One Branch**: You may choose to accept all changes from one branch while discarding the changes from the other branch.
   * **Accepting Changes from Both Branches**: In some cases, you may want to incorporate changes from both branches. This requires careful merging of the conflicting changes to ensure they work together correctly.

5. **Resolving the Conflict**: Implement the chosen resolution strategy by modifying the conflicting files accordingly. This may involve editing the files directly or using tools provided by your version control system to resolve conflicts.

6. **Testing the Resolution**: After resolving the conflict, it's important to test the changes to ensure that they work as expected. This may involve running tests, building the project, or manually verifying the changes depending on the nature of the conflict.

7. **Committing the Resolution**: Once you're satisfied with the resolution, commit the changes to the repository. Include a meaningful commit message that explains the resolution and the reasons behind it.

8. **Completing the Merge**: After resolving all conflicts, complete the merge operation in your version control system to finalize the integration of the branches.

By following these stages, you can effectively resolve merge conflicts and ensure that the changes from multiple branches are successfully integrated.

### Tell me about setting up the repository branch management process

Setting up a repository branch management process is crucial for maintaining organization, collaboration, and version control in software development projects. Here's a step-by-step guide on how to set up a branch management process:

1. **Choose a Version Control System (VCS):** Select a VCS platform like Git, Mercurial, or Subversion. Git is the most popular choice due to its distributed nature and robust features.

2. **Create a Repository:** Set up a central repository where all code changes will be stored. Platforms like GitHub, GitLab, or Bitbucket offer hosting services for repositories.

3. **Define Branching Strategy:** Decide on a branching model that suits your project's needs. Common strategies include Gitflow, GitHub flow, or a custom approach tailored to your team's workflow.

4. **Main Branches:**
   * **Master (or Main):** This branch should contain stable, production-ready code. Direct commits to this branch should be limited and typically done through pull requests.
   * **Development (or Develop):** This branch is where ongoing development work happens. Features are integrated here before being merged into the master branch.

5. **Feature Branches:**
   * Developers create feature branches off the development branch to work on specific features or fixes.
   * Branch names should be descriptive and prefixed with a ticket number or identifier linked to your issue tracking system for traceability.

6. **Pull Requests (PRs):**
   * When a developer completes work on a feature branch, they create a pull request to merge it into the development branch.
   * PRs undergo code review by peers to ensure quality and adherence to coding standards.
   * Continuous Integration (CI) processes, such as automated testing, can be triggered upon opening a PR to catch issues early.

7. **Merge and Deployment:**
   * Once a pull request is approved and passes all checks, it can be merged into the target branch (e.g., development or master).
   * Automated deployment pipelines can be set up to deploy changes to staging or production environments after successful merges.

8. **Release Branches (Optional):**
   * For more structured releases, you may create release branches off the development branch to stabilize features for release.
   * Once a release branch is ready, it can be merged into the master branch for deployment.

9. **Maintenance Branches (Optional):**
   * Long-term support (LTS) releases or bug fixes for older versions can be managed through maintenance branches created off specific release branches.

10. **Documentation:**
    * Document the branching strategy and processes to ensure all team members understand and follow the established guidelines.
    * Include guidelines for branch naming conventions, commit message format, and any specific workflows or tool integrations.

11. **Training and Adoption:**
    * Provide training and guidance to team members on how to use the branching model effectively.
    * Encourage collaboration and communication among team members to ensure smooth integration and delivery of changes.

12. **Iterate and Improve:**
    * Regularly review and refine your branch management process based on feedback and evolving project needs.
    * Continuously monitor and adjust the branching strategy to optimize for efficiency and productivity.

By following these steps, you can establish a robust repository branch management process that promotes collaboration, ensures code quality, and facilitates efficient software delivery.

### Tell us about the branding strategy

Branching strategy is a crucial aspect of Software Configuration Management (SCM), Continuous Integration (CI), and Continuous Deployment (CD) processes. It defines how code changes are managed, integrated, and deployed within a software development project. Several branching strategies exist, each with its own advantages and use cases. Here are some common branching strategies:

1. **Mainline/Branch-per-Feature:**
   * In this strategy, each feature or task is developed on its own branch.
   * Once development is complete, the feature branch is merged back into the mainline (often referred to as the master or trunk branch).
   * This strategy promotes isolation of changes, enabling parallel development of multiple features.
   * However, it can lead to longer-lived branches and potential integration conflicts.

2. **GitFlow:**
   * GitFlow is a branching model popularized by Vincent Driessen.
   * It defines two main branches: master and develop.
   * Feature branches are created off the develop branch, and once complete, they are merged back into develop via pull requests.
   * Releases are made from the develop branch and merged into both develop and master.
   * This strategy provides a clear separation between feature development, releases, and hotfixes, making it suitable for projects with regular releases.

3. **Trunk-Based Development:**
   * In this strategy, there's only one mainline branch (often called trunk or master), and all development is done directly on this branch.
   * Developers work on small, incremental changes and frequently merge their changes into the mainline.
   * This approach encourages continuous integration and fast feedback cycles but requires robust automated testing and deployment pipelines to ensure stability.

4. **Feature Flags/Toggles:**
   * Instead of using separate branches for features, developers introduce feature flags or toggles in the mainline codebase.
   * Features are developed behind these flags, which can be controlled dynamically to enable or disable the feature.
   * This strategy allows for continuous delivery of code changes without branching, but it requires careful management of feature flags and consideration for technical debt.

5. **GitHub Flow:**
   * Similar to GitFlow but simpler, GitHub Flow is often used in projects hosted on GitHub.
   * It revolves around creating short-lived feature branches off the main branch.
   * Once the feature is complete, it's merged back into the main branch via a pull request, triggering CI/CD pipelines.
   * Releases are made directly from the main branch.

The choice of branching strategy depends on factors such as team size, project complexity, release cadence, and organizational preferences. It's essential to select a strategy that aligns with the project's needs while considering scalability, maintainability, and collaboration aspects. Additionally, automation plays a crucial role in supporting the chosen branching strategy by ensuring smooth integration, testing, and deployment processes

### What is CI/CD and what are the benefits for a developer?

CI/CD stands for Continuous Integration/Continuous Delivery (or Continuous Deployment), and it's a set of practices and tools used by software development teams to automate the process of integrating code changes, testing them, and then delivering those changes to production environments.

Here's a breakdown of what each part entails:

1. **Continuous Integration (CI)**: It's the practice of frequently integrating code changes into a shared repository, such as Git, and automatically testing those changes. The key idea is that developers integrate their code changes into the main branch often, usually several times a day. Each integration triggers automated builds and tests to detect integration errors or bugs early in the development process. This ensures that the codebase is always in a deployable state.

2. **Continuous Delivery (CD)**: It's the practice of automatically deploying code changes to testing or staging environments after they have passed through the CI process. The goal is to have a streamlined, automated process for releasing software updates to these environments. Continuous Delivery ensures that code changes are always in a deployable state and ready for production deployment. However, the actual deployment to production is still a manual process in Continuous Delivery.

3. **Continuous Deployment**: This is an extension of Continuous Delivery where every change that passes through the CI/CD pipeline is automatically deployed to production environments without manual intervention. Continuous Deployment takes automation one step further, allowing for faster release cycles and quicker feedback loops.

CI/CD pipelines are typically implemented using a combination of version control systems (like Git), build servers (such as Jenkins, Travis CI, or CircleCI), automated testing frameworks, and deployment automation tools. These pipelines can be customized to fit the specific needs of a development team or project, enabling faster and more reliable software delivery.

Implementing CI/CD practices offers several benefits for developers:

1. **Faster Feedback Loops**: With CI/CD, developers receive immediate feedback on their code changes through automated testing. This rapid feedback loop helps them identify and fix issues early in the development process, reducing the time spent on debugging and troubleshooting later on.

2. **Reduced Integration Issues**: By integrating code changes frequently and automatically, CI ensures that different parts of the codebase work well together. This reduces the likelihood of integration issues and conflicts, making it easier for developers to collaborate and ensuring smoother code integration.

3. **Improved Code Quality**: Continuous testing as part of the CI/CD pipeline helps maintain high code quality standards. Automated tests catch bugs and errors early, ensuring that only well-tested and functioning code is promoted to higher environments.

4. **Increased Productivity**: Automation of repetitive tasks, such as building, testing, and deploying code changes, frees up developers' time to focus on more creative and high-value tasks. Developers can spend less time on manual processes and more time on writing code and solving complex problems.

5. **Faster Time to Market**: CI/CD enables faster and more frequent releases of software updates. With automated testing and deployment, developers can deliver new features and bug fixes to users quickly and reliably, reducing time to market and staying competitive in a fast-paced environment.

6. **Greater Confidence in Releases**: With automated testing and deployment processes in place, developers have greater confidence in the stability and reliability of their releases. They can deploy changes to production with minimal risk, knowing that thorough testing has been performed and that the deployment process is well-controlled.

7. **Continuous Learning and Improvement**: CI/CD encourages a culture of continuous improvement and learning within development teams. By regularly reviewing feedback from automated tests and deployments, developers can identify areas for improvement in their codebase, development processes, and infrastructure, leading to ongoing optimization and refinement.

Overall, implementing CI/CD practices can significantly enhance the developer experience by streamlining development workflows, improving code quality, and accelerating the delivery of software updates to users.

### What are the principles of iterative methodologies?

Iterative methodologies, particularly in the context of Continuous Integration/Continuous Deployment (CI/CD), are founded on several key principles:

1. **Continuous Integration (CI)**:
   * **Frequent Integration**: Developers integrate their code changes into a shared repository frequently, often several times a day.
   * **Automated Builds and Tests**: Automated processes are in place to build and test the integrated code, ensuring that any issues are identified early in the development cycle.
   * **Immediate Feedback**: Developers receive immediate feedback on their changes, allowing them to address any issues quickly.
   * **Version Control**: Utilizing version control systems like Git to manage changes and enable collaboration among team members.

2. **Continuous Deployment (CD)**:
   * **Automated Deployment**: The process of deploying code changes to production or staging environments is automated.
   * **Incremental Updates**: Deployments are done in small increments rather than large batches, reducing the risk associated with changes.
   * **Rollback Mechanism**: There should be mechanisms in place to rollback changes easily in case of failures or issues in production.
   * **Environment Parity**: Ensuring that development, testing, and production environments are as similar as possible to minimize discrepancies and potential deployment issues.

3. **Feedback Loops**:
   * **Short Feedback Loops**: Feedback on code quality, functionality, and deployment should be provided as quickly as possible to enable rapid iteration and improvement.
   * **Monitoring and Logging**: Monitoring systems are in place to detect issues in production environments, and logging is utilized to gather data for analysis and troubleshooting.
   * **User Feedback**: Gathering feedback from users to understand their needs and preferences, which can inform future iterations.

4. **Continuous Improvement**:
   * **Retrospectives**: Regularly reflecting on the development process to identify areas for improvement and implementing changes accordingly.
   * **Metrics and Analytics**: Utilizing metrics and analytics to track performance, identify bottlenecks, and make data-driven decisions for process optimization.
   * **Experimentation and Innovation**: Encouraging experimentation and innovation by providing a safe environment for trying out new ideas and technologies.

5. **Collaboration and Communication**:
   * **Cross-functional Teams**: Encouraging collaboration among developers, testers, operations personnel, and other stakeholders to ensure that everyone is aligned towards common goals.
   * **Transparent Communication**: Open and transparent communication channels to facilitate sharing of information, feedback, and ideas among team members.

By adhering to these principles, teams can create a development and deployment pipeline that is flexible, efficient, and conducive to rapid innovation and improvement.

### 161. What are the advantages and disadvantages of code-convention?

Code conventions, also known as coding standards or coding style guides, are sets of guidelines and rules for writing code in a consistent and readable manner. Here are some advantages and disadvantages of adhering to code conventions:

Advantages:

1. **Readability and Maintainability**: Code conventions help improve the readability of code by making it easier for developers to understand each other's code. Consistently formatted code is also easier to maintain, debug, and update.

2. **Consistency**: Following code conventions ensures that code across a project or team remains consistent. This consistency makes it easier for developers to collaborate, review, and modify code without encountering unexpected formatting or style differences.

3. **Reduced Bugs**: Adhering to code conventions can help reduce the occurrence of bugs by promoting best practices and identifying potential issues early on. For example, consistent naming conventions for variables and functions can help prevent naming-related bugs.

4. **Enforced Best Practices**: Code conventions often include best practices for coding, such as proper commenting, error handling, and code structure. Enforcing these best practices can lead to higher-quality code that is more robust and reliable.

5. **Onboarding New Developers**: Code conventions serve as valuable guides for new developers joining a project or team. By following established conventions, new developers can quickly understand the codebase and contribute effectively without spending excessive time deciphering coding styles.

Disadvantages:

1. **Rigid Enforcement**: Strict adherence to code conventions can sometimes stifle creativity and innovation. Developers may feel constrained by overly rigid rules, leading to resistance or frustration within the team.

2. **Overhead**: Implementing and enforcing code conventions require additional time and effort from developers and teams. This overhead can be significant, especially for larger projects or teams with diverse coding backgrounds.

3. **Subjectivity**: Some aspects of code conventions, such as code formatting and style preferences, can be subjective. Differences in opinion among team members may lead to debates or conflicts over which conventions to follow, potentially hindering productivity.

4. **Learning Curve**: New developers joining a project may need time to familiarize themselves with the code conventions in use. This learning curve can delay their ability to contribute effectively and may require additional training or documentation.

5. **Maintenance**: Code conventions need to be periodically reviewed and updated to reflect changes in coding practices, technologies, or project requirements. Failure to maintain and update conventions over time can lead to inconsistencies or outdated practices in the codebase.

### Explain the CI processes

Continuous Integration (CI) is a software development practice where developers regularly integrate their code changes into a shared repository. Each integration triggers automated build and testing processes to quickly identify and address errors. Here's a breakdown of the CI process:

1. **Version Control System (VCS)**:
   Developers work on their code in their local environments and use a version control system (e.g., Git) to manage changes. They create branches for new features or fixes.

2. **Committing Changes**:
   When developers complete a task or make changes, they commit their code to the repository. Commit messages should be descriptive, explaining the purpose of the changes.

3. **Automated Build**:
   After a commit is made, CI tools like Jenkins, Travis CI, or GitLab CI automatically detect the changes and trigger a build process. During this process, the code is compiled, dependencies are resolved, and artifacts (such as executable files or libraries) are generated.

4. **Automated Testing**:
   Once the build is complete, automated tests are run against the code. These tests can include unit tests, integration tests, and even end-to-end tests depending on the project's requirements. The goal is to ensure that the new changes haven't introduced any regressions or bugs.

5. **Code Quality Checks**:
   In addition to tests, CI pipelines often include static code analysis tools (e.g., SonarQube, ESLint, or Pylint) to check for coding standards, potential bugs, and other issues. This helps maintain consistency and quality across the codebase.

6. **Reporting and Notifications**:
   CI tools provide feedback on the build and test results. Developers are notified of the outcome, including any failures or errors encountered during the process. This allows them to quickly address issues.

7. **Integration with Deployment Pipelines**:
   Depending on the CI/CD (Continuous Integration/Continuous Deployment) setup, successful builds may trigger deployment pipelines. Continuous Deployment (CD) automates the deployment process, allowing changes to be pushed to production environments seamlessly.

8. **Feedback Loop**:
   CI fosters a culture of rapid feedback. Developers receive immediate feedback on their changes, enabling them to iterate quickly and fix issues early in the development cycle.

9. **Continuous Monitoring**:
   CI doesn't stop after the initial build and tests. Continuous monitoring of the codebase and CI pipeline performance helps identify areas for improvement and ensures the stability of the software.

By following CI best practices, development teams can streamline their processes, improve code quality, and accelerate the delivery of reliable software.

### How to edit a commit?

To edit a commit in Git, you typically use the `git rebase` or `git commit --amend` command. Here's how you can do it:

#### Method 1: Using `git commit --amend`

1. **Make changes to your files:**
   First, make the necessary changes to your files in your working directory.

2. **Stage the changes:**
   Once you've made your changes, stage them using:

   ```bash
   git add <file1> <file2> ...
   ```

3. **Amend the commit:**
   Now, use the `--amend` option with `git commit`:

   ```bash
   git commit --amend
   ```

   This command will open your default text editor with the commit message of the last commit. You can edit the commit message if needed. Save and close the editor.

#### Method 2: Using `git rebase`

1. **Make changes to your files:**
   Like before, make the necessary changes to your files in your working directory.

2. **Stage the changes:**
   Stage the changes using:

   ```bash
   git add <file1> <file2> ...
   ```

3. **Rebase interactively:**
   Start an interactive rebase to modify the commit. You can do this by running:

   ```bash
   git rebase -i HEAD~n
   ```

   Replace `n` with the number of commits you want to edit. If you only want to edit the last commit, you can use `HEAD~1`.

4. **Pick the commit to edit:**
   In the interactive rebase editor, change the word `pick` to `edit` in front of the commit you want to modify. Save and close the editor.

5. **Modify the commit:**
   Git will stop at the commit you marked for editing. Make your changes to the files as necessary.

6. **Stage changes and amend the commit:**
   Once you've made your changes, stage them with:

   ```bash
   git add <file1> <file2> ...
   ```

   Then, use the following command to amend the commit:

   ```bash
   git commit --amend
   ```

7. **Continue the rebase:**
   After amending the commit, continue the rebase with:

   ```bash
   git rebase --continue
   ```

   Git will apply any remaining commits after the one you edited.

Remember, amending commits should generally be done for commits that haven't been pushed to a shared repository yet. If you've already pushed the commit, it's better to avoid amending history to prevent conflicts with collaborators who might have already based work on that commit. In such cases, consider creating a new commit with the necessary changes instead.

### Interactive rebase

Interactive rebase is a powerful feature in Git that allows you to rewrite the commit history of a branch. It lets you combine, edit, delete, and reorder commits interactively. This is particularly useful for cleaning up your commit history before pushing changes to a shared repository, making it easier for others to understand your changes.

Here's a basic overview of how to perform an interactive rebase:

1. **Start the interactive rebase**: First, ensure you're on the branch you want to rebase. Then, run the following command:

    ```bash
    git rebase -i <base>
    ```

    Replace `<base>` with the commit or branch you want to rebase onto. For example, if you're rebasing onto the `main` branch, you'd replace `<base>` with `main`.

2. **Edit commits interactively**: After running the command, a text editor will open with a list of commits from your branch. Each commit will have a prefix (e.g., `pick`, `edit`, `squash`, `reword`, etc.) indicating the action Git will perform on that commit during the rebase.

    * `pick`: Use this to keep the commit as is.
    * `edit`: Use this to pause the rebase process at this commit, allowing you to make changes.
    * `squash` or `fixup`: Use these to combine the commit with the previous one.
    * `reword`: Use this to change the commit message.

3. **Save and close the editor**: Make your changes to the list of commits as needed, save the file, and close the editor.

4. **Resolve any conflicts**: If Git encounters any conflicts during the rebase process, it will pause and ask you to resolve them manually. After resolving conflicts, you can continue the rebase process by running `git rebase --continue`.

5. **Finish the rebase**: Once you've resolved all conflicts and made any desired changes, complete the rebase by running:

    ```bash
    git rebase --continue
    ```

6. **Push changes (if necessary)**: If you've rebased commits that have already been pushed to a remote repository, you may need to force-push your changes using:

    ```bash
    git push origin <branch> --force
    ```

It's important to note that interactive rebasing rewrites commit history, so it should only be done on branches that you haven't shared with others or branches that you're certain others are okay with being rewritten.
