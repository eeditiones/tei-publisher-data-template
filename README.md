# tei-publisher-data-template

Use this template to set up your own data app to be used with TEI Publisher, Publisher-generated application or any custom app.

Separating your data from application code has many benefits, particularly for actively developed applications and data sets. This way changes to your code can be deployed without redeploying and reindexing your data and vice versa. It is also easier to maintain separate repositories (e.g. in Git) and only grant certain privileges separately to editorial and developer teams.

NB: you'll need to edit the corresponding variable(s) in `modules/config.xqm` in your application package.

Nevertheless, some projects may prefer to still keep their data integrated with the application in a single .xar package.

## TEI Publisher

After forking/cloning this template repository, create a `data` subdirectory and fill it with your documents.

You will **have to** change the namespace for your data package as well as its title and target collection. Replace `app-data` in the following files:

* repo.xml - change `meta/target` to correspond to the collection your data app will be installed to
* expath-pkg.xml 
   - change `package/@abbrev` to correspond to the collection your data app will be installed to 
   - set `package/@name` with your data package namespace
   - edit the `title` element to describe this package; it will be shown in the eXist-db Dashboard

NB: starting with TEI Publisher 9 we recommend using the following namespace pattern: `http://teipublisher.com/ns/data/{app}-data` for *data* packages, where `{app}` should be replaced with your application name (corresponding to `expath-pkg.xml: package/@abbrev` of the *application* package).

Other files in the template you may need to change:

* collection.xconf - collection configuration file for your data
    - adjust Lucene index, facets and fields definitions to suit your application
    - if using other namespaces, make sure to add these on `index`; TEI and DocBook namespaces are added by default
* index.xql - a function module by default imported into Lucene index via `<module uri="http://teipublisher.com/index" prefix="nav" at="index.xql"/>`. Adjust functions to suit your application. When changing this module remember to reindex the data collection for the changes to be reflected by the indexes.
* build.xml - build file, used to create a xar package with ant
* pre-install.xql - store index configuration 
* post-install.xql - prepare the data collections
