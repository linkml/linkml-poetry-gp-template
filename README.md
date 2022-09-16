__THIS REPOSITORY IS ARCHIVED__

For creating new projects, you should use this:

https://github.com/linkml/linkml-project-cookiecutter

# LinkML Project Template

_A template for LinkML projects_

NOTE: You don't need to use this repository directly as a GitHub template!

Instead:

 * [install poetry](https://python-poetry.org/docs/)
 * [install linkml](https://linkml.io/linkml/intro/install.html)
 * run `linkml-ws new`

## Example:


```
mkdir ~/my-projects
cd ~/my-projects
pip install linkml
linkml-ws new my-project-name
cd my-project-name
# edit src/linkml/my-project-name
make setup
```

Type `make` to see a full list of options.

Then you will be encouraged to run
```shell
cd my-project-name
make setup
```

This will give you a fully functional LinkML repository with artifact generation via github actions based on the 
example "Person" schema that comes with this template.  The next steps are to replace the example yaml files in
`src/linkml` with your own model files.

Sometimes you may wish to divide your model into modules in individual yaml files.  Or, you may be starting a 
project using linkml-ws with an existing set of schema yaml files from an autogenerated schema. This may mean that you
have more thank one .yaml file in your_project/src/linkml/schema directory.  However, in order for the project generation
scrips to work, you must provide one yaml "root" file as the starting point to generate your schema.  In order to make
this work, you must declare a "root" schema.yaml file that imports your submodules.

For example, if my schema is divided into domains like this:

```bash
my_project/src/linkml/my_schema_domain_1.yaml
my_project/src/linkml/my_schema_domain_2.yaml
my_project/src/linkml/my_schema_domain_3.yaml
```

adding a simple:
```bash
myschema.yaml 
```

with the contents:
```bash
- id: myschema
- name: myschema
imports:  
- linkml:types
- my_schema_domain_1
- my_schema_domain_2
- my_schema_domain_3
````

and setting your schema file to `myschema.yaml` in the `about.yaml`, linkml-ws will find and properly iterate through
all three domains of your model generating the artifacts as you have indicated in your `gen-project` makefile target.

## How to author a schema

There are several ways to author a LinkML model.  

* If you have an existing JSONSchema or OWL representation of your data, try using `schema-automator`.  This
  LinkML tool allows automatic conversion between JSONSchema, RDF, OWL and 
  LinkML YAML: https://linkml.io/schema-automator/intro/cli.html
* If you are more comfortable declaring schemas in google sheets or excel, check out `schemasheets` (also a LinkML
  tool): https://linkml.io/schemasheets/
* hand author your model in YAML by editing the files generated in src/linkml/
  * We recommend pycharm as a convenient multipurpose editor of YAML.  pycharm allows you to include the 
    LinkML meta model as a schema source which provides validation of model component use 
    just like it notifies you of python syntax or style errors.  For more information on configuring a JSONSchema 
    for reference in pycharm, see: https://www.jetbrains.com/help/pycharm/json.html#ws_json_schema_add_custom


## Getting it into GitHub

- Create a new repo but don't allow GH to initialize any files for you: no README, no .gitignore, no license, etc. Just give it a `Repository name` and click `Create repository`
- set your origin, based on your GH org or user name and your new repo's name
  - `git remote add origin git@github.com:<USER/ORG>/<REPO NAME>.git`
- push!
  - `git push -u origin main`


## Alternative protocol

You can also simply clone this repo and use it as a template, modifying files as you need - however,
this is no longer the recommended path


