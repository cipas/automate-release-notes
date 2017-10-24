# How To: automate github release notes creation

## Things you need

1. commitizen + cz-conventional-changelog
2. conventional-github-releaser

### 1. Install commitizen and adapter, usage.
**Note**: If you already have commitizen setup go to number *[2](#workflow)*

```
$ npm install -g commitizen
$ cd project
$ npm install --save-dev commitizen
$ commitizen init cz-conventional-changelog --save-dev --save-exact
```

You need to set the preferred cz adapter:

```
$ echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```

Now use `git cz` instead of `git commit`

You can add an npm script in your package.json and when you want to commit use `npm run cm`:

```
"scripts": {
  "cm": "git add -A && git cz"
}
```

### 2. Install convetions-github-releaser, usage

Create a new token and set your environment variable `CONVENTIONAL_GITHUB_RELEASER_TOKEN` to the token you just created. The scopes for the token you need is `public_repo` or `repo` (if you need to access private repos).

```
$ npm install -g conventional-github-releaser
$ cd my-project
$ conventional-github-releaser -p angular
```

## Workflow

- start feature `git flow feature start`
- do changes
- commit `npm run cm`
- repeat
- `npm version patch`
- push ( don't forget --tags; `git push origin BRANCH --tags` | `git push --tags`)
- `conventional-github-releaser -p angular` | for private repos you need to use `convetional-github-releaser -t OAUTH_TOKEN -p angular`
