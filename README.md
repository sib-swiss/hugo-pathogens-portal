# Hugo Pathogens Portal Theme

### [Hugo](https://gohugo.io) pathogens portal theme inspired by the [Swedish Pathogens Portal](https://www.pathogens.se/)

![Screenshot](https://raw.githubusercontent.com/sib-swiss/hugo-pathogens-portal/main/images/screenshot.png)

- [Requirements](#requirements)
- [Installation](#installation)
- [Customisation](#customisation)
- [Menu](#menu)
- [Dashboards](#dashboards)
- [Events](#events)
- [News](#news)
- [Configuration](#configuration)
- [Versioning](#versioning)
- [Credits](#credits)
- [Contributing](#contributing)

## Requirements

- Hugo 0.124 or higher

## Installation

### Install as git submodule
Navigate to your hugo project root and run:

```
git submodule add https://github.com/sib-swiss/hugo-pathogens-portal themes/hugo-pathogens-portal
```

Then run hugo (or set `theme = "hugo-pathogens-portal"`/`theme: hugo-pathogens-portal` in configuration file)

```
hugo server --minify --theme hugo-pathogens-portal
```

### Install as hugo module

You can also add this theme as a Hugo module instead of a git submodule.

Start with initializing hugo modules, if not done yet:
```
hugo mod init github.com/repo/path
```

Navigate to your hugo project root and add [module] section to your `hugo.toml`:

```toml
[module]
[[module.imports]]
path = 'github.com/sib-swiss/hugo-pathogens-portal'
```

Then, to load/update the theme module and run hugo:

```sh
hugo mod get -u
hugo server --minify
```

### Creating site from scratch

Below is an example on how to create a new site from scratch:

```sh
hugo new site myportal; cd myportal
git init
git submodule add https://github.com/sib-swiss/hugo-pathogens-portal themes/hugo-pathogens-portal
cp -R themes/hugo-pathogens-portal/exampleSite/content/* ./content
```

```sh
hugo server --minify --theme hugo-pathogens-portal
```

## Customisation

### Logo

To add your own logo, create a `static/images/portal.png` file in your Hugo site. The logo will overwrite the default logo.

### Favicon

To add your own favicon, create a `static/images/favicon.ico` file in your Hugo site. The favicon will overwrite the default favicon.

## Menu

### Main Menu

The main menu is generated from the content files in the `dashboards` directory, the `tags` taxonomy, and the manually defined menu items.

Whenever you add a new content file in the `dashboards` directory, a new item will be added to the main menu.

Whenever you add a new tag to either a content file inside the `dashboards` directory or a content file in the `news` directory, a new item will be added to the main menu.

Finally, to add a new item to the menu, simply specify `main` in the front matter of the content file:

```yaml
menu:
    main:
        name: "Research"
        identifier: "research"
```

If you wish that the menu item is expandable, you can use the `identifier` from the menu item as the parent identifier:

```yaml
menu:
    research:
        name: "Infectious diseases"
        identifier: "infectious-diseases"
```

### Navigation Menu

The navigation menu is display at the top right of the page.
  
To add entries to the navigation menu, you can add the following to the front matter of a content file:
  
```yaml
menu:
  navbar_top:
        name: "About"
        identifier: "about"
```

### Footer Menu

The footer menu is displayed at the bottom of the page.

#### About

To add entries to the about section of the footer menu, you can add the following to the front matter of a content file:

```yaml
menu:
  footer_about:
        name: "About"
        identifier: "about"
```

#### Data

To add entries to the data section of the footer menu, you can add the following to the front matter of a content file:

```yaml
menu:
  footer_data:
        name: "Data"
        identifier: "data"
```

## Dashboards

Dashboards are displayed on the main page and can be filtered by tags.

To add a new dashboard, create a new markdown file in the `content/dashboards` directory. If you want to host the dashboard directly in your HUGO site, you will need to write the content of the dashboard in the markdown file. If you want to redirect to an external site, you can add the `redirect_url` parameter to the front matter of the markdown file.

Also, if you want to highlight a dashboard, you can add the `highlight: true` parameter to the front matter of the markdown file.

Finally, you can add tags to the dashboard by adding the `tags` parameter to the front matter of the markdown file.

```yaml
---
title: "Infectious diseases dashboard"
description: "Information on cases of infection and illness in Switzerland and the Principality of Liechtenstein caused by various pathogens, provided by the Federal Office of Public Health."
image: dashboards/image.png
redirect_url: https://www.idd.bag.admin.ch/
highlight: true
tags:
    - Surveillance
    - Infectious diseases
---
```

## Events

Events are displayed on the main page and can be filtered by categories.

To add a new event, create a new markdown file in the `content/events` directory.

Make sure to always add the following front matter to the markdown file:

```yaml
---
title: "My event"
start_date: 2024-09-02T08:00:00Z
end_date: 2024-09-04T17:00:00Z
location: Geneva, Switzerland
description: This is a description of my event.
organiser: SIB Swiss Institute of Bioinformatics
external_url: https://www.sib.swiss/
categories:
  - Training
  - NGS
---
```

Your events will then be automatically displayed on the main page. If the event is already over, it will be shown under the past events section.

## News

News are displayed on the main page and can be filtered by tags.

To add a new news, create a new markdown file in the `content/news` directory.

Make sure to always add the following front matter to the markdown file:

```yaml
---
title: "My news"
date: 2024-08-28T13:03:06+02:00
draft: false
author: "John Doe"
image: news/image.png
tags:
  - COVID-19
---
```

Keep in mind that the `draft` parameter is set to `true` by default. If you want to display the news on the main page, you will need to set it to `false`. Also, the `date` parameter is mandatory, if the `date` is in the future, the news will not be displayed.

## Configuration

### Site Configuration

You can configure the site by editing the `config.toml` file in the root of your Hugo site.

Here is an example configuration:

```toml
baseURL = "http://localhost/"
title = "Pathogens Portal"
theme = "hugo-pathogens-portal"

# (Optional) Set this to true to enable 'Last Modified by' date and git author
#  information on 'doc' type pages.
# enableGitInfo = true

# Specify the default content language.
defaultContentLanguage = "en"

# Multilingual mode config
# There are different options to translate files
# See https://gohugo.io/content-management/multilingual/#translation-by-filename
# And https://gohugo.io/content-management/multilingual/#translation-by-content-directory
# [languages]
# [languages.en]
# languageName = "English"
# languageCode = "en"
# contentDir = "content"
# weight = 1

[params]
    # (Optional) Set source repository location.
    # Used for 'Last Modified' and 'Edit this page' links.
    # repository = "https://github.com/sib-swiss/hugo-pathogens-portal"
    
    # (Optional) Enable 'Edit this page' links for 'doc' page type.
    # Disabled by default. Uncomment to enable. Requires 'BookRepo' param.
    # Path must point to the site directory.
    # editPath = 'edit/main/exampleSite'
    
    # (Optional) Set the logo for your institution next to the pathogens-portal logo.
    # logo = "images/logo.png"
    
    # (Optional) Set the external link for the logo of your institution.
    # homepage = "https://www.google.com"
    
    # (Optional) Set the email to contact you
    # mail = ""
    
    # (Optional) Set the social media links for your institution.
    # twitter = ""
    # linkedin = ""
    
    # (Optional) Set the country to retrieve stats from the central pathogens-portal.
    # This is used to retrive several stats from the central pathogens-portal using the API
    # and filtering by your configured country.
    # country = "Switzerland"
    
    # (Optional) Set the country to retrieve publications from the Europe PMC API.
    # This is used to retrieve publications from the Europe PMC API and filtering by your configured country.
    # pubmed_country = "Switzerland"
    
    # (Optional) Set the URL of your national biobank to display the link on the homepage.
    # biobank_url = ""
```

### Multi-Language Support

Theme supports Hugo's [multilingual mode](https://gohugo.io/content-management/multilingual/), just follow configuration guide there.

## Versioning

This theme follows a simple incremental versioning. e.g. `v1`, `v2` and so on. There might be breaking changes between versions.

If you want lower maintenance, use one of the released versions. If you want to live on the bleeding edge of changes, you can use the `main` branch and update your website when needed.

## Credits

This theme is based on the [Swedish Pathogens Portal](https://www.pathogens.se/) (SciLifeLab Data Centre (2024) pathogens-portal v2.2.1) [Zenodo](https://zenodo.org/doi/10.5281/zenodo.10629602), with funding from the [BY-COVID project](https://by-covid.org/). 

The source code of the Swedish Pathogens Portal is available on [GitHub](https://github.com/ScilifelabDataCentre/pathogens-portal).

This theme is developed by the [SIB Swiss Institute of Bioinformatics](https://www.sib.swiss/).

## Contributing

Contributions are welcome and will be fully credited. We accept contributions via Pull Requests on [GitHub](github.com/sib-swiss/hugo-pathogens-portal).

Feel free to open issues if you find missing configuration or customisation options.