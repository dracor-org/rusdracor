# RusDraCor
## Corpus Description
We are building a Russian Drama Corpus with files encoded in
[TEI-P5](http://www.tei-c.org/Guidelines/P5/). Our corpus comprises
**91 plays** to date, stemming from [ilibrary](http://ilibrary.ru/),
[Wikisource](https://ru.wikisource.org/), [РВБ](http://rvb.ru/) and
[lib.ru](http://lib.ru/), converted to TEI and corrected by us. There
will be more.

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
to use our API. If you have [jq](http://blog.librato.com/posts/jq-json)
installed, it would work like this:

```
for play in `curl 'https://dracor.org/api/corpus/rus' | jq -r ".dramas[] .id"`; do
    wget -O "$play".csv https://dracor.org/api/corpus/rus/play/"$play"/networkdata/csv
done
```

The API info page is at `https://dracor.org/api/info`.

## Simple Visualisation with R

To have a first look at the distribution of the number of speakers per play over
time, you could feed the metadata table into R:

```
library(data.table)
library(ggplot2)
rusdracor <- fread("https://dracor.org/api/corpus/rus/metadata.csv")
ggplot(rusdracor[], aes(x = year, y = numOfSpeakers)) + geom_point()
```

Result:

![number of speakers per play over time](numOfSpeakers.png)

(README last updated on June 3, 2018.)
