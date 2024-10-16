# How to convert the Google Cloud documentation site navigation interface into Markdown TOC syntax

Convert the unselectable navigation interface of the Google Cloud documentation site into Markdown TOC for further processing.

<https://gitlab.com/brlin/gcloud-docs-nav2md>  
[![The GitLab CI pipeline status badge of the project's `main` branch](https://gitlab.com/brlin/gcloud-docs-nav2md/badges/main/pipeline.svg?ignore_skipped=true "Click here to check out the comprehensive status of the GitLab CI pipelines")](https://gitlab.com/brlin/gcloud-docs-nav2md/-/pipelines) [![GitHub Actions workflow status badge](https://github.com/brlin-tw/gcloud-docs-nav2md/actions/workflows/check-potential-problems.yml/badge.svg "GitHub Actions workflow status")](https://github.com/brlin-tw/gcloud-docs-nav2md/actions/workflows/check-potential-problems.yml) [![pre-commit enabled badge](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white "This project uses pre-commit to check potential problems")](https://pre-commit.com/) [![REUSE Specification compliance badge](https://api.reuse.software/badge/gitlab.com/brlin/gcloud-docs-nav2md "This project complies to the REUSE specification to decrease software licensing costs")](https://api.reuse.software/info/gitlab.com/brlin/gcloud-docs-nav2md)

\#google-cloud \#data-conversion \#html-query

## Prerequisites

You need to have the following software installed in order to follow this tutorial:

* gzip  
  For uncompressing the gzip-compressed product's release archive.
* [html-query](https://github.com/orf/html-query)  
  For parsing the navigation interface HTML markup into JSON data for further processing.
* [jinjanator](https://github.com/kpfleming/jinjanator)  
  For converting the JSON navigation data into Markdown markup using Jinja2 templates.
* [jq](https://jqlang.github.io/jq/)  
  For beautifying the JSON navigation data for easier inspecting the parse results.
* Mozilla Firefox  
  For selecting the HTML markup of the navigation interface we need to parse data from.
* Your preferred plaintext editor application  
  For examining the HTML markup.
* Your preferred tar archive manipulating application.  
  For extracting the product's release archive.
* Your preferred text terminal emulator application  
  For running command-line interface commands required by this tutorial.

## Process

Execute the following instructions to do the conversion:

1. Download the release archive from [the Releases page](https://gitlab.com/brlin/gcloud-docs-nav2md/-/releases).
1. Extract the release archive.
1. Launch Mozilla Firefox.
1. Browse [the main page of the Google Cloud documentation website](https://cloud.google.com/docs/).
1. Right click the first item in the navigation interface(it is "Google Cloud Documentation home" at the writing of this process at 2024/10/16), and select Inspect.  The developer console will open, and, in the main panel of the Inspector tab you should notice a `devsite-nav-text` class element is selected.
1. Search outward the nested elements until you locate an element that is in the `devsite-nav-list` class, right-click the element and select the Copy > Inner HTML option in its contextual menu.
1. Create a dump.html file in the /path/to/the/extracted/product/gcloud-docs-nav2md-_X_._Y_._Z_ folder, the content is similar to [this sample file](dump.sample.html).
1. Use your preferred text editor to open the file, and paste the previously copied HTML markup to the file, then save the file.
1. Launch your preferred terminal emulator application.
1. Change the working directory to the /path/to/the/extracted/product/gcloud-docs-nav2md-_X_._Y_._Z_ folder.
1. Run the following commands to convert the navigation interface HTML markup to JSON data:

    ```bash
    hq \
        '{
            navitems: .devsite-nav-item
                | [ {
                    title: .devsite-nav-text | @text,
                    url: a | @(href)
                    }
                ]
        }' <dump.html \
        | jq . \
        | tee nav.json
    ```

   The conversion result should be similar to [this sample file](nav.sample.json).
1. Run the following commands to convert the navigation JSON data to ToC Markdown markup:

    ```bash
    jinjanate_opts=(
        --format json
        --output toc.md
    )
    jinjanate "${jinjanate_opts[@]}" toc.md.j2 nav.json
    ```

   The conversion result should be similar to [this sample file](toc.sample.md).

After doing so you should have your ToC Markdown markup in the toc.md file([sample](toc.sample.md))!

## References

The following materials are referenced during the development of this project:

* [Special query syntax | orf/html-query: jq, but for HTML](https://github.com/orf/html-query?tab=readme-ov-file#special-query-syntax)  
  Explains the usage of the `@(href)` and the `@text` query syntax of html-query.

## Licensing

Unless otherwise noted(individual file's header/[REUSE.toml](REUSE.toml)), this product is licensed under [version 3 of the GNU Affero General Public License](https://www.gnu.org/licenses/agpl-3.0.en.html), or any of its recent versions you would prefer.

This work complies to [the REUSE Specification](https://reuse.software/spec/), refer the [REUSE - Make licensing easy for everyone](https://reuse.software/) website for info regarding the licensing of this product.
