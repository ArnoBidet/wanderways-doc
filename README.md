# Wanderways-Doc

## Setting up

To run this project on your machine, follow those steps :
- Install [python](https://www.python.org/downloads/) (you may need to restart your computer aftewards)
- Install [pip](https://pip.pypa.io/en/stable/installation/) (Pip Install Packages)
- Install [mkdocs](https://www.mkdocs.org/user-guide/installation/)
- Install [material theme ](https://squidfunk.github.io/mkdocs-material/getting-started/)
- Install [markdown](https://python-markdown.github.io/) to support internal links
- Install [syntax highlighting](https://pygments.org/download/)
- Install [mkdocs-render-swagger-plugin](https://github.com/bharel/mkdocs-render-swagger-plugin) for swagger rendering plugin
In a script (minus python install) : 
```sh
python -m ensurepip --upgrade
pip install mkdocs mkdocs-material markdown Pygments mkdocs-render-swagger-plugin
```

## Uploading

To upload the documentation, use the command :

`mkdocs gh-deploy`