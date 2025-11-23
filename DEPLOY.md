## How to Deploy

### Preliminaries

GitHub-specific naming convention is as follows:

+ `user-remote`: The remote for your GitHub homepage repository
  `<your-github-username>.github.io`.
+ `my-changes`: The main working branch where you make changes specific to
  your information and different from the `master` (sometimes `main`) branch. 
+ `sync`: The branch in sync with upstream and used to pull upstream changes.

### Deploying using GitHub actions

1. Commit all the changes in the `my-changes`.
2. Merge the branches in the `master` branch using `--strategy-option theirs`.
3. Push the master branch to the `user-remote`.

### Manually deploying as a user page

1. Add the remote of user repository
    ```bash
    $ git remote add <user-remote> <url>
    ```
    If the user repository remote is already added, verify it using:
    ```bash
    $ git remote -v
    ```

2. Set the value of `url` and `baseurl` in `_config.yml` as follows:
    ```markdown
    url: #empty
    baseurl: #empty
    ```

3. Commit and push all the changes to a branch, `<my-changes>`.

4. Run command:
    ```bash
    $ ./bin/deploy -s <my-changes> --no-push
    ```
    By default, the above command compiles and deploys the changes to branch, `gh-pages`.

5. Force push the deployed branch, `gh-pages` to the user page repository.
    ```bash
    $ git push <user-remote> gh-pages:master -f
    ```
6. The webpage should be up at `username.github.io`.

### Manually deploying as a project page

1. Set the value of `url` and `baseurl` in `_config.yml` as follows:
    ```markdown
    url: #empty
    baseurl: <github-project-name>
    ```

2. Commit and push all the changes to a branch, `<my-changes>`.

3. Run command:
    ```bash
    $ ./bin/deploy -s <my-changes>
    ```
4. The webpage should be up at `username.github.io/<github-project-name>`.

### Update from upstream

Check if the `upstream` remote exits. 
```bash
$ git checkout <sync>
$ git fetch upstream
$ git merge <sync>
$ git checkout <master>
$ git merge <latest_tag_name>
```