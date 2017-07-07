Document Management
===================


Abstract
--------

This document tries to explore how to build a distributed document management
system using Web Standards.

We envision a system where all the meta-information is stored within the HTML
as structured RDFa elements, allowing easy navigation with automatic
reference and glossary management.


Document structure
------------------

For each document, multiple HTML files are provided:

 * the main document which includes all the document content;
 * an index file that just contains the abstract plus meta-information
   (e.g. author, title, keywords);
 * an optional summary page which imports the index file of the main document and
   of all referenced documents to provide a nice overview page.

The index file is not meant to be viewed directly by browsers, it just
consolidates all the meta-information about the document and is
imported by both the main document and the summary page.
This index file is the key to be able to relate between documents even
when they are managed by different organizations.


Detailed design
---------------

The index file is an HTML file containing RDFa meta-data.
It should only have minimal external dependencies so that it can be loaded quickly.
This is important because a large number of index files may have to be loaded to
generate information about referenced documents.

The index file defines as an RDF resource using the
[https://www.w3.org/TR/vocab-dcat/ Data Catalog Vocabulary]
The document itself should be represented as one `dcat:Dataset` ressource.

The following information is recommended to be provided for the document:

* Author(s) (`dcterms:creator`);
* Title(s) (`dcterms:title`);
* Keywords (`dcterms:subject`);
* Table of contents (`dcterms:tableOfContents`);
* Abstract of the document (`dcterms:abstract`);
* Link to the summary page (`dcat:landingPage`).


Styling the document
--------------------

Provide a document template as HTML-import.
Customizable properties can be provided via CSS custom variables.

The template should already provide both the template for print
as well as a version for interactive use.


Styling the summary
-------------------

TBD

References to other documents
-----------------------------

By importing the .index.html of all referenced documents, it is possible to
include meta-information about these documents.
(E.g. show a list of references, show hover information / footnotes with a
summary of referenced items.)

By not importing the complete referenced document (with its own further links),
we can prevent the client from fetching unneeded (and potentially very large)
documents.

Each document reference is represented as on <link rel="import" is="gain-reference" name="..."> import.
The `name` is used as identifier when referencing the reference.
TBD: defaults


References to specific items
----------------------------

References to other documents are only allowed when there is already a
document-level reference.


Backlinks from other documents
------------------------------

Requires an external index which is obviously dependent on the other documents.
This index would have to be managed by some document management system.



Figures
-------

TBD


Interaction with Paged Media
----------------------------

The `@page` CSS tag only works in the toplevel, not within a web component.
Basic page setup for the selected document template has to be done
as `<style>` within a HTML-import.

TBD


Specification of index files
----------------------------

TBD

Relation to HtmlBook
--------------------

TBD
