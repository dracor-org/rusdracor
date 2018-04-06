# RusDraCor

We are building a Russian Drama Corpus with files encoded in
[TEI-P5](http://www.tei-c.org/Guidelines/P5/). Our corpus comprises **89 plays**
so far (April 2018), stemming from [ilibrary](http://ilibrary.ru/),
[Wikisource](https://ru.wikisource.org/), [РВБ](http://rvb.ru/) and
[lib.ru](http://lib.ru/), converted into TEI and corrected by us. There will be
more.

If you just want to download the corpus in its current state, do this:

`svn export https://github.com/dracor-org/rusdracor/trunk/tei`

RusDraCor was first presented on June 29, 2017, at the [Corpora 2017
conference](https://events.spbu.ru/events/anons/corpora-2017/?lang=Eng) in St.
Petersburg ([our slides here](https://dlina.github.io/presentations/2017-spb/))
and on July 11, 2017, at the ["Digitizing the stage"
conference](https://digitizingthestage.wordpress.com/) in Oxford. The social
network data we extracted so far can also be explored with [our
Shinyapp](https://shiny.dracor.org/).

## API

An easy way to download the network data (instead of the actual TEI files) is
to use our API, like so:

```
for file in tei/*.xml; do
    fn=`basename $file | cut -d'.' -f1`
    wget -O csv/"$fn".csv https://dracor.org/api/corpus/rus/play/"$fn"/networkdata/csv
done
```
In this example, the script has to be executed in the directory under ```tei/```
(which has to be checked out, of course) – CSV data will be written to ```csv/```.
