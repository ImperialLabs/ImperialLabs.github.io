
# SLAPI Documentation Site

## How to Update

### Pages

-   Update Pages
    -   All site pages are under the [pages](pages) directory in this repo
    -   Each folder represents a section on the left hand sidebar menu on the doc site
    -   Just adjust the markdown (.md) file you want and save, then commit and push. Github pages will automatically regenerate the site
-   Add Pages
    -   Under the [pages](pages) directory, select the section you wish to add page to
    -   Copy the file `new_page.md` from [pages/new_page.md](pages/new_page.md) to the section of your choice and rename (**Important**: use the naming scheme `section_pagetopic.md` for the new file)
    -   The new_page.md will have instruction on where to edit and what to leave alone
    -   When the new page is ready, make sure to add it to the [_data/sidebars/framework_sidebar.yml](_data/sidebars/framework_sidebar.yml) file
        -   Under the section you are create a page for, add the following

            ```yaml
            - title: New Page
              url: /new_page.html # Notice the switch here to html? You are telling it to generate this file from the .md file
              output: web
            ```
    -   Just commit and push, then the new page should be on the site

### Sections
-   Add Section
    -   When adding a new section you'll need to do the following
        -   Create a new folder under [pages](pages) with the section name
        -   Add the new section to the [_data/sidebars/framework_sidebar.yml](_data/sidebars/framework_sidebar.yml) file

            ```yaml
            # Note: Wherever you place this in the yaml is where it will show up on the sidebar
            - title: New Section
              output: web
              folderitems:
                # If adding pages too
                - title: New Page
                  url: /new_page.html
                  output: web
            ```
