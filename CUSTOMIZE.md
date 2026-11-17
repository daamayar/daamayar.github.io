# Customize

Here we will give you some tips on how to customize the website. One important thing to note is that **ALL** the changes you make should be done on the **main** branch of your repository. The `gh-pages` branch is generated automatically and should not be edited manually.

## Project structure

The project is structured as follows, focusing on the main components that you will need to modify:

```txt
.
├── 📂 assets/: contains the assets that are displayed in the website
│   └── 📂 json/
    │   └── 📄 resume.json: CV in JSON format (https://jsonresume.org/)
├── 📂 _bibliography/
│   └── 📄 papers.bib: bibliography in BibTeX format
├── 📄 _config.yml: the configuration file of the template
├── 📂 _data/: contains some of the data used in the template
│   ├── 📄 cv.yml: CV in YAML format, used when assets/json/resume.json is not found
│   └── 📄 repositories.yml: users and repositories info in YAML format
├── 📂 _includes/: contains code parts that are included in the main HTML file
│   └── 📄 news.liquid: defines the news section layout in the about page
├── 📂 _layouts/: contains the layouts to choose from in the frontmatter of the Markdown files
├── 📂 _news/: the news that will appear in the news section in the about page
├── 📂 _pages/: contains the pages of the website
|   └── 📄 404.md: 404 page (page not found)
├── 📂 _posts/: contains the blog posts
├── 📂 _projects/: contains the projects
└── 📂 _sass/: contains the SASS files that define the style of the website
    ├── 📄 _base.scss: base style of the website
    ├── 📄 _cv.scss: style of the CV page
    ├── 📄 _distill.scss: style of the Distill articles
    ├── 📄 _layout.scss: style of the overall layout
    ├── 📄 _themes.scss: themes colors and a few icons
    └── 📄 _variables.scss: variables used in the SASS files
```

## Configuration

The configuration file [\_config.yml](_config.yml) contains the main configuration of the website. Most of the settings is self-explanatory and we also tried to add as much comments as possible. If you are not sure about a setting, just keep the default value.

> Note that the `url` and `baseurl` settings are used to generate the links of the website, as explained in the [install instructions](INSTALL.md).

All changes made to this file are only visible after you rebuild the website. That means that you need to run `bundle exec jekyll serve` again if you are running the website locally or push your changes to the repository if you are using GitHub Pages.

## Modifying the CV information

There are currently 2 different ways of generating the CV page content. The first one is by using a json file located in [assets/json/resume.json](assets/json/resume.json). It is a [known standard](https://jsonresume.org/) for resumes.

What this means is, if there is no resume data defined in [_config.yml](_config.yml) and loaded via a json file, it will load the contents of [_data/cv.yml](_data/cv.yml). If you want to use the JSON data, make sure your file matches its schema.

## Modifying the user and repository information

The user and repository information is defined in [_data/repositories.yml](_data/repositories.yml). You can add as many users and repositories as you want. Both informations are used in the `repositories` section of the homepage.

## Creating new pages

You can create new pages by adding new Markdown files in the [_pages](_pages/) directory. The easiest way to do this is to copy an existing page and modify it. You can choose the layout of the page by setting the `layout` property in the front matter.

## Creating new blog posts

To create a new blog post, you can add a new Markdown file in the [_posts](_posts/) directory. The [name of the file must follow](https://jekyllrb.com/docs/posts/#creating-posts) the format `YYYY-MM-DD-title.md`.

If you want to create blog posts that are not ready to be published, but you want to track it with git, you can create a [_drafts](https://jekyllrb.com/docs/posts/#drafts) directory and store them there.

## Creating new projects

You can create new projects by adding new Markdown files in the [_projects](_projects/) directory. The easiest way to do this is to copy an existing project and modify it.

## Adding some news

You can add news in the about page by adding new Markdown files in the [_news](_news/) directory. There are currently two types of news: inline news and news with a link. News with a link take you to an external page when clicked.

## Adding Collections

This Jekyll theme implements `collections` to let you break up your work into categories. The theme comes with two default collections: `news` and `projects`. Items from the `news` collection are displayed in the homepage and on the blog.

You can easily create your own collections, apps, short stories, courses, or whatever your creative work is. To do this, edit the collections in the [_config.yml](_config.yml) file, create a corresponding directory, and add your files there.

## Adding a new publication

To add publications create a new entry in the [_bibliography/papers.bib](_bibliography/papers.bib) file. You can find the BibTeX entry of a publication in Google Scholar by clicking on the quotation mark icon next to the paper.

You can add extra information to a publication, like a PDF file in the `assets/pdfs/` directory and add the path to the PDF file in the BibTeX entry with the `pdf` field. Some of the supported fields include `abstract`, `bibtex_show`, `blog`, `pdf`, `slides`, `website`, and `selected`.

### Author annotation

In publications, the author entry for yourself is identified by string array `scholar:last_name` and string array `scholar:first_name` in [_config.yml](_config.yml). For example, if you have the following configuration:

```yaml
scholar:
  last_name: [Einstein]
  first_name: [Albert, A.]
```

If the entry matches one form of the last names and the first names, it will be underlined. Keep meta-information about your co-authors in [_data/coauthors.yml](_data/coauthors.yml) and Jekyll will highlight them automatically.

```yaml
"adams":
  - firstname: ["Edwin", "E.", "E. P.", "Edwin Plimpton"]
    url: https://en.wikipedia.org/wiki/Edwin_Plimpton_Adams

"podolsky":
  - firstname: ["Boris", "B.", "B. Y.", "Boris Yakovlevich"]
    url: https://en.wikipedia.org/wiki/Boris_Podolsky

"rosen":
  - firstname: ["Nathan", "N."]
    url: https://en.wikipedia.org/wiki/Nathan_Rosen

"bach":
  - firstname: ["Johann Sebastian", "J. S."]
    url: https://en.wikipedia.org/wiki/Johann_Sebastian_Bach

  - firstname: ["Carl Philipp Emanuel", "C. P. E."]
    url: https://en.wikipedia.org/wiki/Carl_Philipp_Emanuel_Bach
```

If the entry matches one of the combinations of the last names and the first names, it will be highlighted and linked to the url provided. Note that the keys **MUST BE** lower cased and **MUST NOT** contain accents. This is because the keys are used to match the last names in the BibTeX entries, considering possible variations.

### Buttons (through custom bibtex keywords)

There are several custom bibtex keywords that you can use to affect how the entries are displayed on the webpage:

- `abbr`: Adds an abbreviation to the left of the entry. You can add links to these by creating a venue.yaml-file in the \_data folder and adding entries that match.
- `abstract`: Adds an "Abs" button that expands a hidden text field when clicked to show the abstract text
- `altmetric`: Adds an Altmetric badge (if a DOI is provided, just use `true`; otherwise add the altmetric identifier here and the link is generated automatically)
- `annotation`: Adds a popover info message to the end of the author list that can potentially be used to clarify superscripts. HTML is allowed.
- `arxiv`: Adds a link to the Arxiv website (Note: only add the arxiv identifier here - the link is generated automatically)
- `bibtex_show`: Adds a "Bib" button that expands a hidden text field with the full bibliography entry
- `blog`: Adds a "Blog" button redirecting to the specified link
- `code`: Adds a "Code" button redirecting to the specified link
- `dimensions`: Adds a Dimensions badge (if a DOI or PMID is provided, just use `true`; otherwise only add the Dimensions identifier here - the link is generated automatically)
- `html`: Inserts an "HTML" button redirecting to the user-specified link
- `pdf`: Adds a "PDF" button redirecting to a specified file (if a full link is not specified, the file will be assumed to be placed in the /assets/pdf/ directory)
- `poster`: Adds a "Poster" button redirecting to a specified file (if a full link is not specified, the file will be assumed to be placed in the /assets/pdf/ directory)
- `slides`: Adds a "Slides" button redirecting to a specified file (if a full link is not specified, the file will be assumed to be placed in the /assets/pdf/ directory)
- `supp`: Adds a "Supp" button to a specified file (if a full link is not specified, the file will be assumed to be placed in the /assets/pdf/ directory)
- `website`: Adds a "Website" button redirecting to the specified link

You can implement your own buttons by editing the [_layouts/bib.liquid](_layouts/bib.liquid) file.

## Changing theme color

A variety of beautiful theme colors have been selected for you to choose from. The default is purple, but you can quickly change it by editing the `--global-theme-color` variable in the [_sass/_base.scss](_sass/_base.scss) file.

## Adding social media information

You can add your social media links by adding the specified information at the `Social integration` section in the [_config.yml](_config.yml) file. This information will appear at the bottom of the page.

## Adding a newsletter

You can add a newsletter subscription form by adding the specified information at the `newsletter` section in the [_config.yml](_config.yml) file. To set up a newsletter, you can use a service like Mailchimp or ConvertKit.

Depending on your specified footer behavior, the sign up form either will appear at the bottom of the `About` page and at the bottom of blogposts if `related_posts` are enabled, or in the footer area of the site.

## Adding Token for Lighthouse Badger

To add secrets for lighthouse-badger, create a [personal access token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token) and add it as a repository secret named `LIGHTHOUSE_BADGER_TOKEN`.

Also In case you face the error: "Input required and not supplied: token" in the Lighthouse Badger action, this solution resolves it.

### Personal Access Token (fine-grained) Permissions for Lighthouse Badger:

- **contents**: access: read and write
- **metadata**: access: read-only

Due to the necessary permissions (PAT and others mentioned above), it is recommended to use it as a secret rather than an environment variable.

## Customizing fonts, spacing, and more

You can customize the fonts, spacing, and more by editing [_sass/_base.scss](_sass/_base.scss). The easiest way to try in advance the changes is by using [chrome dev tools](https://developer.chrome.com/docs/devtools/).

## Scheduled Posts

`al-folio` contains a workflow which automatically publishes all posts scheduled at a specific day, at the end of the day (23:30). By default the action is disabled, and to enable it you need to enable the workflow in GitHub Actions.

In order to use this you need to save all of your "Completed" blog posts which are scheduled to be uploaded on a specific date, in a folder named `_scheduled/` in the root directory.

> Incomplete posts should be saved in `_drafts/`

### Name Format

In this folder you need to store your file in the same format as you would in `_posts/`

> Example file name: `2024-08-26-This file will be uploaded on 26 August.md`

### Important Notes

- The scheduler uploads posts everyday at 🕛 23:30 UTC
- It will only upload posts at 23:30 UTC of their respective scheduled days, It's not uploaded in 23:59 in case there are a lot of files as the scheduler must finish before 00:00
- It will only upload files which follow the pattern `yyyy-mm-dd-title.md`
  - This means that only markdown files will be posted
  - It means that any markdown which do not follow this pattern will not be posted
- The scheduler works by moving posts from the `_scheduled/` directory to `_posts/`, it will not post to folders like `_projects/` or `_news/`
- The date in the name of the file is the day that file will be uploaded on
  - `2024-08-27-file1.md` will not be posted before or after 27-August-2024 (Scheduler only works for posts scheduled on the present day)
  - `2025-08-27-file2.md` will be posted exactly on 27-August-2025
  - `File3.md` will not be posted at all
  - `2026-02-31-file4.md` is supposed to be posted on 31-February-2026, but there is no 31st in February hence this file will never be posted either
