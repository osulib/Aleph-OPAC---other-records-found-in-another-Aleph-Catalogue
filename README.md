# Aleph-OPAC - other records found in another Aleph Catalogue

## Introduction
For cooperating libraries, both with ALEPH system, their OPAC is enriched with link to another Aleph OPAC with number of records found according to user's query in another (remote) catalogue. This tip to another OPAC can be added to short results page, as well as to "nothing found" pages for simple search.

Example in short results page:

![](https://github.com/matyasbajger/Aleph-OPAC---other-records-found-in-another-Aleph-Catalogue/blob/master/not-found-example.jpg)

## Requirements
Aleph version 18-23, X-Server

## Workflow
User's query is taken from Aleph OPAC placeholders to Javascript variables. Using AJAX (asynchronyous HTTP) another - remote ALEPH is queries, if contains records relative to the query. This can be done directly from user's device by Javascript, if X-Server find function is free open on Internet. Otherwise, admin can set redirection from Javascript through home Aleph server, which must be set as accessible/allowed to remote X-server service find.
If X-Server returns some results (non-zero), script fills the determined place (div element) with information that some records are to be found in another catalogue together with link to this search in the remote OPAC.

## Implementation

### 1. Short results page
To web/opac template `short-tail` add an empty element, where results - info and link to remote OPAC will be added:

`<div id="otherAleph-el" ></div>

Somewhere after, add javascript search the remote Aleph and constructing info to html page. See code page: [short-tail](https://github.com/matyasbajger/Aleph-OPAC---other-records-found-in-another-Aleph-Catalogue/blob/master/short-tail) that includes comments for initial set up too.

### 2. Nothing found pages for simple search
`find-b-list*` and `find-b-permute-*` templates (the first for one word queries, another for more words)

Add following line storing Aleph placeholder to Javascript variable to "head" templates  `find-b-list-head` and `find-b-permute-head`. Line/code can be added at any place in these templates:
  
`<script type="text/javascript">var request_notfound="100";var request_ccl_code="200";</script>`

Similarly like in short-tail above, add target display html element acd script to templates `find-b-list-tail` and `find-b-permute-tail`. See code for both in code [find-b-list-tail](https://github.com/matyasbajger/Aleph-OPAC---other-records-found-in-another-Aleph-Catalogue/blob/master/find-b-list-tail) , including instructions for initial set up in comments.


### Redirection CGI script
If you would use redirection of calling remote X-server through your home aleph server, save the file [redir.cgi](https://github.com/matyasbajger/Aleph-OPAC---other-records-found-in-another-Aleph-Catalogue/blob/master/redir.cgi) to your cgi-script home directory, might it be: `$httpd_root/cgi-bin/redir.cgi`
Make this file executable: `chmod +x redir.cgi`


***

### Created by
Matyas Franciszek Bajger, University of Ostrava Library library.osu.eu, Moravian-Silesian Research Library in Ostrava www.svkos.cz
bajger@svkos.cz
Live at: https://aleph.osu.cz  https://katalog.svkos.cz

### Licence
GNU GPL 3.0
