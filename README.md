# Svelte template: AP Men's Basketball

## To get started

Run `npm run scrape` to update the data. Publishing commands are as normal.

### Using degit

`degit` is a package that makes copies of a git repository's most recent commit. This allows for generating the scaffolding from this template directly from the command line.

Since this is a private repository, you'll need to set up SSH keys with your Github account. More information on how to do that [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

To install degit: `npm install -g degit`

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit axiosvisuals/ap-mbb-poll --mode=git test-app
cd test-app
```

### Using 'Use this template'

Click the `Use this template` button above and follow the instructions prompted by GitHub.

### Post-clone setup

In your local repo:

- Install the dependencies: `npm install`
- ~~Update `project.config.json` with your project's title and slug (TODO: make this automatic)~~
- Ctrl+F the term `[insert slug]` and replace it with your project slug. Also update the page title by ctrl+F'ing `[insert name]` and replacing it with a project name. (Or, you can manually update these in `public/index.html` and `project.config.json`.)
- Start the development server: `npm run dev`
- Navigate to [localhost:5000](http://localhost:5000). The app should run and update on changes.

### Modifying the table

- Table column names can be edited in `App.svelte`. At a minimum, each column must have a `label` and `visible` property.

```js
  const cols = [
    {
      label: "Rank", // Column Label
      visible: false, // Whether the label is visible or not
    },
    {
      label: "Logo",
      visible: false,
      ariaHidden: true, // Whether the column is visible to screen readers or not
    },
    {
      label: "Team",
      visible: false,
      class: "team", // Any additional classes the `<th>` cell will have
    },
    {
      label: "W-L",
      visible: true,
      ariaLabel: "Win-Loss Record", // Text the screen reader should read
    },
    ...
  ];
```

- `isSplitTable` is a `Boolean` and defines whether or not a single table should be split into two halves on larger screens.

## Publishing

- Make sure your changes are committed to `master`
- `gulp publish` will push to `master`, build the app, and then deploy the built version to the S3 bucket specified in `project.config.json`
  - You'll be prompted to see if you want to generate fallbacks (for this to work, you'll need to have [localhost:5000](http://localhost:5000) running in another tab), they'll go in `public/fallbacks`
