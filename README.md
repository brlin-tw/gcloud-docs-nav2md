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
* jinjanator  
  For converting the JSON navigation data into Markdown markup using Jinja2 templates.
* jq  
  For beautifying the JSON navigation data for easier inspecting the parse results.
* Mozilla Firefox  
  For selecting the HTML markup of the navigation interface we need to parse data from.
* Your preferred plaintext editor application  
  For examining the HTML markup.
* Your preferred tar archive manipulating application.  
  For extracting the product's release archive.
* Your preferred text terminal emulator application  
  For running command-line interface commands required by this tutorial.

## Licensing

Unless otherwise noted(individual file's header/[REUSE.toml](REUSE.toml)), this product is licensed under [version 3 of the GNU Affero General Public License](https://www.gnu.org/licenses/agpl-3.0.en.html), or any of its recent versions you would prefer.

This work complies to [the REUSE Specification](https://reuse.software/spec/), refer the [REUSE - Make licensing easy for everyone](https://reuse.software/) website for info regarding the licensing of this product.
