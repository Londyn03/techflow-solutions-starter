# Workflow Analysis

## 1. What triggers this workflow to run?
The workflow triggers on a `push` to the `main` branch, and also on `pull_request` 
events targeting `main`. This means it runs automatically whenever code is pushed 
directly to main, or whenever a pull request is opened against main.

## 2. What are the four main steps this workflow performs?
1. Checkout code
2. Validate HTML files
3. Check for broken links
4. Deploy to GitHub Pages

## 3. What does the "Checkout code" step do and why is it necessary?
It uses the `actions/checkout` action to pull the repository's code into the GitHub 
Actions runner's virtual environment. It's necessary because the runner starts with 
an empty environment — without this step, there would be no files for later steps 
(HTML validation, link checking, deployment) to act on.

## 4. What is the purpose of the environment configuration?
It defines the environment the deployment targets (GitHub Pages) and the permissions 
the job needs to publish the site. This scopes what the workflow is allowed to do and 
lets GitHub track deployment history and the resulting live URL for that environment.

## 5. How does this automated deployment improve reliability compared to manual deployment?
It removes human error and inconsistency — the same checks (HTML validation, link 
checking) run identically every time, and deployment only happens automatically if 
all checks pass. There's also a full audit log of every deploy (who, when, what 
changed, pass/fail status), which manual deployment doesn't guarantee since it 
depends on someone remembering every step correctly each time.

## 6. What would happen if you pushed code to a different branch (not main)?
Nothing would deploy. Since the trigger is scoped to the `main` branch, pushes to 
any other branch would not run this workflow's deploy step at all — the code would 
sit on that branch until it's merged into `main`, which is exactly the point of 
protecting the branch that triggers production deployments.