(credits)=
# Credits and License

You can refer to this book as:

> Tom van Woudenberg and Iuri Rocha from Delft University of Technology (2026) _Matrix method in statics_. https://oit.tudelft.nl/CIEM5000/2026. Source files at https://github.com/TUDelft-books/CIEM5000

You can refer to individual chapters or pages within this book as:

> `<Title of Chapter or Page>`. In Tom van Woudenberg and Iuri Rocha from Delft University of Technology (2026) _Matrix method in statics_. https://oit.tudelft.nl/CIEM5000/2026/<relative link to page>. Source files at https://github.com/TUDelft-books/CIEM5000: `./book/<path to file(s)>` chapter, accessed `date`.

We anticipate that the content of this book will change significantly during the run of this course. Therefore, we recommend using the source code directly with the citation above that refers to the GitHub repository and lists the date and name of the file. Although content will be added over time, chapter titles and URL's in this book are expected to remain relatively static. However, we make no guarantee, so if it is important for you to reference a specific location/commit within the book.

The most recent complete version of this book is the [2024/2025 version of this book](https://oit.tudelft.nl/CIEM5000/2025/).

## How the book is made

This book is created using open source tools: it is a [TeachBook](https://teachbooks.io/) that is written using Markdown and Jupyter notebooks. The files are stored on a [public GitHub repository](https://github.com/TUDelft-books/CIEM5000). The website can be viewed at https://oit.tudelft.nl/CIEM5000/2026/. View the repository README file or contact the authors for additional information.

To recreate the website you have two options (more information in the [TeachBooks manual](https://teachbooks.io/manual/):
- In the GitHub interface: fork this repository, enable Github Pages from the source GitHub actions (Settings - Code and automation - Pages - Build and deployment - Source - GitHub Actions), enable workflows (Actions - I understand my workflows, go ahead and enable them) and run the call-deploy-book workflow (Actions - call-deploy-book - Run workflow - Run workflow). The website is released on the URL as shown on the workflow summary when the workflow has finished (Actions - call-deploy-book - call-deploy-book - Summary).
- On your own computer: clone this repository, install the required packages (`pip install -r requirements.txt`) and build the book (`teachbooks build book`). The website is stored locally in `book/_build/index.html`.

## License
This book is [CC BY 4.0 licensed](https://creativecommons.org/licenses/by/4.0/) allowing you to share and adapt the material, as long as the source is named. External resources that are reused in this book are listed below.

(external_resources)=
## External resources
 Page [](./lecture2/fem.ipynb) includes code from {cite:t}`MUDE`. Original content is licensed under CC BY. 
