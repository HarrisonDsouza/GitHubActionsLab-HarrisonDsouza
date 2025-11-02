# GitHub Actions Lab - Harrison Dsouza

## Workflow 1: Dependent Jobs Workflow

### Purpose
This workflow demonstrates how to create job dependencies so that jobs run in a specific order: build → test → deploy. It simulates a real deployment pipeline where each stage must complete successfully before the next one starts.

### Key Concepts Demonstrated
- **needs**: Creates dependencies between jobs to control execution order
- **runs-on**: Specifies which operating system the job runs on (ubuntu-latest)
- **steps**: Defines the individual tasks within each job

### Challenges and Solutions
Initially, I wasn't sure how to make jobs wait for each other. I learned that without the `needs` keyword, all jobs run in parallel. Once I added `needs: build` to the test job and `needs: test` to the deploy job, the workflow executed in the correct sequence.

---

## Workflow 2: Environment Variables and Secrets

### Purpose
This workflow shows how to use environment variables at different scope levels (workflow, job, and step) and how to securely store and access sensitive information like AWS credentials using GitHub Secrets.

### Key Concepts Demonstrated
- **env**: Environment variables defined at workflow, job, and step levels
- **secrets**: Secure storage for sensitive data that gets automatically masked in logs
- **runs-on**: Uses ubuntu-latest as the runner
- Variable scope hierarchy and how each level can access variables from above

### Challenges and Solutions
The syntax for accessing variables and secrets was confusing at first. I had to learn that environment variables use `${{ env.VARIABLE_NAME }}` while secrets use `${{ secrets.SECRET_NAME }}`. After practicing with both, the pattern became clear. Also, GitHub's automatic masking of secrets in logs was a nice security feature I hadn't expected.

---

## Workflow 3: Multi-Platform Testing

### Purpose
This workflow runs tests simultaneously across three different operating systems (Ubuntu, Windows, and macOS) to ensure code compatibility across platforms.

### Key Concepts Demonstrated
- **runs-on**: Different values for each platform (ubuntu-latest, windows-latest, macos-latest)
- **Parallel execution**: Jobs without `needs` run simultaneously
- **needs**: Deliberately omitted to allow parallel execution
- Platform-specific commands for different operating systems

### Challenges and Solutions
The main challenge was handling OS-specific commands. Linux and macOS use `uname -a` and `cat`, while Windows uses `systeminfo` and `type`. I had to adjust the commands for each platform.

Also, I initially forgot to add the `.yml` extension to the workflow file, which caused GitHub Actions not to recognize it. Once I renamed it to `multi-platform.yml`, the workflow appeared and ran correctly.
