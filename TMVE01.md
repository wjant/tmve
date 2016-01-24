This project has moved to: https://github.com/ajbc/tmve-original

# TMVE 0.1 #
A copy of the html version of this page that accompanies the source can be found [here](http://www.princeton.edu/~achaney/tmve/wiki100k/browse/topic-presence.html).

## Demo ##
This [browser](http://www.sccs.swarthmore.edu/users/08/ajb/tmve/wiki100k/browse/topic-list.html) was produced by using the results of running David Blei's LDA-C on 100,000 Wikipedia articles to find 50 topics.

## Tutorial ##
First, download build LDA-C and run it on a dataset. For the above demo, the command looked something like:
```
./lda est 1/50 50 settings.txt wiki/100K/word_count.dat seeded wiki-100k-lda
```
Next, the LDA data will need to be processed and put into a database; for this purpose, use the database generator provided in the lib folder. Again, for the demo, the command to run the generator would be as follows.
```
python generate_db.py 100k_wiki_db wiki/100K/word_count.dat wiki-100k-lda/final.beta wiki-100k-lda/final.gamma wiki/100K/vocab.dat wiki/100K/dmap.dat
```
This can take a while for large datasets. As a short-cut, a demo 1k database is included in the demo folder, entitled 1k\_demo\_db.

Finally, TMVE needs to be run with a project file, which specifies what database and template to use. Templates control how the data is displayed; in this case, a basic browser is produced. The included project file wiki\_project\_demo.tmv is set up to run with the demo database.

The command to run TMVE with the demo project is fairly simple:
```
python src/tmve.py demo/wiki_project.tmv
```
Or, for more information as the script runs, the verbose mode is helpful:
```
python src/tmve.py -v demo/wiki_project.tmv
```
For the demo project, you will need to be connected to the Internet while TMVE generates the document pages as it must pull content from Wikipedia. When this is done, you should have a local browser (in the demo directory) like the demo above, but a little smaller.

## Making Changes ##
Creating a new template will allow you to view your data in an alternative fashion. To do so, take a look at the BasicBrowser template included in the TMVE source download.

To use another dataset, you will need to change the way documents are displayed. This is currently hard-coded into the BasicBrowser.py file, in the function get\_doc\_display.

To try different topic models, only the database generator needs to be changed. Depending on how the output differs from LDA-C, the work to do this may be minimal.