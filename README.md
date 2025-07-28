# Photography Journey Blog Site
#### Video Demo URL:  <(https://youtu.be/RGvPKLLFyw0)>
#### Description: I created a blog website to document my photography journey and progress


## Project Structure:

├── admin/
│   ├── config.yml           # Netlify CMS configuration
│   └── index.html           # CMS admin interface
├── _includes/
│   └── header.html          # Header template included in layout.html and blog_layout
├── _layouts/
│   └── layout.html          # Main site template
│   └── blog_layout.html     # Blog site template
├── _posts/                  # Blog posts
│   └── 2025-07-10-test.md
│   └── 2025-07-20-Hua_Hin.md
│   └── 2025-07-25-First-Film.md
├── assets/
│   └── uploads/             # Blog images collection
│       └── Film
│       └── Hua_Hin
│   └── home_images/         # Homepage carousel images
│   └── css/                 # Custom stylesheets
├── index.md                 # Homepage content
├── contact.md               # Contact page
├── contact_success.html     # Contact success page
├── _config.yml              # Jekyll configuration
├── netlify.toml             # Netlify build settings
├── Gemfile                  # Ruby dependencies
├── search.json              # (unfinished) for site-wide future search feature
└── README.md                # This file


## Site Information
This site was built in jekyll (Ruby-based static site generator) using HTML, CSS, Bootstrap and JavaScript.

Jekyll version: `4.4.1`
Ruby version: `3.4.4`

## Accessing the site

### Method 1: Local Host
Run `bundle exec jekyll serve` in the root folder (/final_project)
may need to run `bundle install` if some configuration updates required

### Method 2: Netlify test deployment site
site URL: [bespoke-sunflower-51a633.netlify.app](https://bespoke-sunflower-51a633.netlify.app)

The folder for this deployment was _site/ folder generated from running
`bundle exec jekyll serve` in a local host.

This version works with email contact form which has `data-netlify="true"` attribute in it (contact.html), so contact_success.md can be accessed.

## Accessible pages:

### 1. Main Site

#### 1.1 Homepage
Contains 3 images in a bootstrap carousel slideshow which can be clicked left and right
The images are saved in `/assets/home_images/`

#### 1.2 About me
Contains a picture of me and a brief description of the website

#### 1.3 Blogs
Display previews for blogs in the form of bootstrap cards with latest blog on the top left of the page

Each blog card has blog category displayed as card badges. Each blog can be accessed with Readmore button.
The 3 current blogs are saved in `_posts/` as markdown files

This page also has a sidebar to filter blog categories.
The side bar was created based on this W3.CSS Sidebar example: https://www.w3schools.com/w3css/tryit.asp?filename=tryw3css_sidebar
Press the 3 stripes button to open and close button to close the sidebar.

The sidebar has a search bar which can search any text in any blog. This was done with each blog card containing full blog content but hidden from the card with `<div class="full-content" data-full-content="{{ post.content | strip_html | escape }}"></div>`
but information can still be accessed with JavaScript code. Blogs with content matching search query remain visible while others become hidden. The search bar work in real-time search as well as by submitting the button or press enter.
Test search: "long exposure" -> only Hua Hin card has this content.


It also has 2 checkboxes: film and digital.
When neither checkboxes are checked and when both are checked, all blog cards are displayed.
When one of the checkboxes is checked, blog cards with category unchecked will be hidden.

#### 1.4 Contact
Left half displays social media icons (Facebook, Youtube, Instagram).
Currently only instagram icon is linked to my photography account: https://www.instagram.com/noobshooter_bkk/

Right half displays a contact form which takes `data-netlify` attribute
If all fields in the contact form are filled with correct type,
submitting the form will redirect to `/contact_success/` page
Contact form data submitted can be accessed on my Netlify dashboard.

#### 1.5 Contact Success
Displays quick message that user has submitted the contact form successfully

### 2. CMS Admin Page
can be accessed with URL: [bespoke-sunflower-51a633.netlify.app/admin/](https://bespoke-sunflower-51a633.netlify.app/admin/)

At the moment this page is a test-repo does not require logins
New blog posts with pictures can be created and publish here without touching any codes.

The `config.yml` file in `admin/` determine the layout of the blog,
using `blog_layout.html` in `_includes/`.
As this `config.yml` has test-repo backend, posts created won't get saved to github.
It will be changed to this for the real site deployment:

```yaml
backend:
    name: github
    repo: my-username/project-repo-name
    branch: main
```

## Use of Jekyll reusable layouts:
All the pages accessible on the navigation bar have consistent
layout with the same header and navigation bar.

This was done with jekyll syntax (`header.html` in `_includes/` and `layout.html` in `_layouts/`)

Navigation bar has site-wide search button which expands a searchbar when clicked as a potential future feature to be work with the (unfinished) search.json file.

## Stylesheets
These are the stylesheet links included in `layout.html`:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<link rel="stylesheet" href="https://www.w3schools.com/w3css/5/w3.css">
```








