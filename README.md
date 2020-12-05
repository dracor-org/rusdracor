# RusDraCor
## Corpus Description
We are building a Russian Drama Corpus with files encoded in
[TEI-P5](http://www.tei-c.org/Guidelines/P5/). Our corpus comprises
**211 plays** to date, originating from [ilibrary](https://ilibrary.ru/),
[Wikisource](https://ru.wikisource.org/), [РВБ](https://rvb.ru/),
[lib.ru](http://lib.ru/), [ФЕБ](http://feb-web.ru/),
[СовЛит](http://www.ruthenia.ru/sovlit/) and
[Wikilivres](https://wikilivres.org/), converted to TEI and corrected
and enhanced by us. There will be more.

If you want to cite the corpus, please use this publication:

- **Fischer, Frank, et al. (2019)**. Programmable Corpora: Introducing DraCor, an Infrastructure for the Research on European Drama. In *Proceedings of DH2019: "Complexities"*, Utrecht University, [doi:10.5281/zenodo.4284002](https://doi.org/10.5281/zenodo.4284002).

RusDraCor was first presented on June 29, 2017, at the [Corpora 2017
conference](https://events.spbu.ru/events/anons/corpora-2017/?lang=Eng) in St.
Petersburg ([our slides here](https://dlina.github.io/presentations/2017-spb/)),
on July 11, 2017, at the ["Digitizing the stage"
conference](https://digitizingthestage.wordpress.com/) in Oxford and
on November 14, 2017, at the
[TEI 2017 conference](https://hcmc.uvic.ca/tei2017/abstracts/t_115_fischeretal_lifeonstage.html)
in Victoria. The social network data we extract from plays may also be explored
on our website [dracor.org/rus](https://dracor.org/rus) or via
[our Shinyapp](https://shiny.dracor.org/).

If you just want to download the corpus in its current state in XML-TEI,
do this:

`svn export https://github.com/dracor-org/rusdracor/trunk/tei`

## API

An easy way to download the network data (instead of the actual TEI files) is
to use our API ([documentation here](https://dracor.org/doc/api)).
If you have [jq](https://blog.appoptics.com/jq-json/) installed, it would work
like this:

```
for play in `curl 'https://dracor.org/api/corpora/rus' | jq -r ".dramas[] .name"`; do
    wget -O "$play".csv https://dracor.org/api/corpora/rus/play/"$play"/networkdata/csv
done
```

The API info page is at `https://dracor.org/api/info`.

## Simple Visualisation with R

To have a first look at the distribution of the number of speakers per play over
time, you could feed the metadata table into R:

```
library(data.table)
library(ggplot2)
rusdracor <- fread("https://dracor.org/api/corpora/rus/metadata.csv")
ggplot(rusdracor[], aes(x = yearNormalized, y = numOfSpeakers)) + geom_point()
```

Result:

![number of speakers per play over time](numOfSpeakers.png)

Here is a barplot showing the number of plays per decade:

![number of plays per decade](playsPerDecade.png)

(README last updated on December 5, 2020.)
