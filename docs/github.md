# Linking Your PE Account to Your GitHub Account

## Prerequisites

1. You should already have your SoC Unix account, cluster access, and SoC VPN set up, and be able to `ssh` into one of the PE hosts.  If you are not able to do this, please look at the guide on [programming environments](environments.md).
2. You should feel comfortable running basic UNIX commands.  If you have not gone through the UNIX guide and got your hands dirty, please [look at the guide and play with the various basic Unix commands](unix/essentials.md).
3. You should already have a GitHub account and can log into [GitHub.com](https://www.github.com).
4. {++You have set up Vim according to [the set up instruction](vim/setup.md)++}

## Purpose

You will be using `git` (indirectly) for retrieving skeleton code and submitting completed assignments.  We will set up your accounts on a PE host below so that `git` will be associated with your GitHub account.  This is a one-time setup.  You don't have to do this for every programming exercise.

## 1. Setting up `.gitconfig`

Run the following commands to configure `git`:

```Bash
git config --global user.name <your name>
git config --global user.email <your email>
git config --global github.user <your github user name>
```

Your email should be whatever you used to sign up on GitHub (which may not be your SoC or NUS email).

For example, 

```
git config --global user.name "Ah Beng"
git config --global user.email "ahbeng@example.com"
git config --global github.user "ahbeng67"
```

After the above, you can check if the configuration is set correctly by running the following commands:

```
git config --get github.user
```

It should print your GitHub username as already set.  If there is a typo, you can rerun the corresponding command to edit the configuration.

You can also check the file `~/.gitconfig` by running:
```
cat ~/.gitconfig
```

It should show something like:
```
[user]
    name = Ah Beng
    email = ahbeng@example.com
[github]
    user = ahbeng67
```

## 2. Setting up Password-less Login

- Login to [GitHub.com](https://www.github.com) using your account.  Ensure that you are using the account you registered for CS2030S.

- Go to the URL [https://github.com/settings/tokens](https://github.com/settings/tokens). Alternatively, Click on Your Profile Avatar -> Settings -> Developer Settings -> Personal Access Tokens -> Tokens (classic)

   The page should say "Personal access tokens (classic)" at the top.


- Click on "**Generate new token**" (on the top-right), then **Generate new token (classic)**  You will be asked to enter the following information:

   - **Note**: Enter something meaningful to you to explain what this token is for
   - **Expiration**: Set a **Custom** duration that covers until the end of the semester (e.g., 15/05/2027)
   - **Select scopes**: Select "**repo**" (all the subscopes will be selected automatically)

After setting the above, click on the "**Generate token**" button at the bottom of the page.  

Your personal access token will be created.  Copy-paste this to somewhere safe and private. We will be using it in the next step.

Students who are actively using GitHub for other work and prefer to have finer control over the token permissions may choose to create fine-grain personal access token instead, and configure its permission to your personal preference.

## 3. Accept and Retrieve Ex0 from GitHub

For this to work, you must first be added to the Classroom50 Organization.  Note that this platform is a replacement for GitHub classroom and there may be some incompatibility.  Unfortunately, GitHub classroom is now permanently retired.  Please ask your issue in Ed as we try this new platform.

### 3.1 Accept the Assignment

- Go to [Classroom50](https://classroom50.org/).  Sign-in with your registered GitHub account.
- Once you have been added to the organization, go to the current semester organization page.  Click "Open" button.
- Go to "Exercise" assignment.  Click "View assignments" button.
- Accept the assignment.  New assignments will appear once they are released.  For now, there should be "ex0".
    - Click "Accept assignment" button from the corresponding assignment.  This will bring you to another page.
    - Click "Accept assignment" button again.  This time, it will be bigger and at the bottom.  You can also look at the exercise description.
    - Your repository will now be set up.

### 3.2 Configure the PE Host to Store Your Credentials

- Connect to pelogin.  Run the following command.
    ```Bash
    git config --global credential.helper store
    ```
    - This step ensures that your GitHub credentials (username and personal access token) will be stored securely on the PE host so that you don't have to enter them every time you interact with GitHub.

### 3.3 Retrieve the Exercise

- Navigate to your preferred directory, or create a new directory for your current semester CS2030S exercise.
- Run the "get" script from CS2030S directory.
    ```Shell
    /opt/course/cs2030s/get <ex>
    ```
    - Replace `<ex>` with the desired exercise (e.g., `ex0`).
- If this is your first time, you will be asked for your username and password.
    - Username is your **GitHub username**.
    - Password is your **token** from step 2 above.
         - Note that there will be nothing shown on the screen when you type your token.  Just paste it and press Enter.
- If everything works well, the exercise should be cloned into the current directory.

### 3.4 Submitting the Exercise

- Work on the exercise.  We **highly recommend** working on pelogin as you will be using a similar setup for your practical exam.
    - We will not be answering questions related to the environment during the practical exam.
    - Please make sure that you are familiar with the environment.
- Navigate to your exercise directory.
- Run the "submit" script from CS2030S directory.
    ```Shell
    /opt/course/cs2030s/submit <ex>
    ```
    - Replace `<ex>` with the desired exercise (e.g., `ex0`).

!!! bug "No Submission"

    Your submission will not be made if

    - there is no change in your submission;
    - there is a compilation error in your submission;
    - there is a failing test case (which may be a private test case) in your submission; or
    - other issues.

    If you see an error message similar to the following, it means there is no change in your submission.
    ```Text
    On branch submit-history
    Untracked files:
    (use "git add <file>..." to include in what will be committed)
            : <list of files>

    nothing added to commit but untracked files present (use "git add" to track)
    ❗️  Failed to commit to submit-history
    ```