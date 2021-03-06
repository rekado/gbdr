# gbdr
genome browsing with dalliance

This is a sketch for a [htmlwidget](https://htmlwidgets.org) wrapper for JavScript genome browser [dalliance](https://biodalliance.org).

# Quick guide

A dalliance function call generates a genome browser htmlwidget with a given reference genome (eg. GRCh38) and a given gene annotation (eg. GENCODEv21):

```{}

dalliance() 

```


<script language="javascript" src="http://www.biodalliance.org/dev/dalliance-compiled.js"></script>
<script language="javascript">
  new Browser({
    chr:          '14',
    viewStart:    75276274,
    viewEnd:      75284730,
    cookieKey:    'human',
    coordSystem: {
      speciesName: 'Human',
      taxon: 9606,
      auth: 'GRCh',
      version: '38'
    },
    
    
    sources:     [{name:                 'GRCh38',      
                   twoBitURI:            'http://www.biodalliance.org/datasets/hg38.2bit',  
                   tier_type:            'sequence',
                   provides_entrypoints: true}
                   
                  ,{name: 'GENCODEv21',
                       desc: 'Gene structures from GENCODE 21',
                       bwgURI: 'http://www.biodalliance.org/datasets/GRCh38/gencode.v21.annotation.bb',
                       stylesheet_uri: 'http://www.biodalliance.org/stylesheets/gencode2.xml',
                       collapseSuperGroups: true,
                       trixURI: 'http://www.biodalliance.org/datasets/GRCh38/gencode.v21.annotation.ix'}
   
                ]});
    
</script>

<div id="svgHolder"></div>

<br><br>

The corresponding javascript would look like this:

```{}

<script language="javascript" src="http://www.biodalliance.org/dev/dalliance-compiled.js"></script>
<script language="javascript">
  new Browser({
    chr:          '14',
    viewStart:    75276274,
    viewEnd:      75284730,
    cookieKey:    'human',
    coordSystem: {
      speciesName: 'Human',
      taxon: 9606,
      auth: 'GRCh',
      version: '38'
    },
    
    
    sources:     [{name:                 'GRCh38',      
                   twoBitURI:            'http://www.biodalliance.org/datasets/hg38.2bit',  
                   tier_type:            'sequence',
                   provides_entrypoints: true}
                   
                  ,{name: 'GENCODEv21',
                       desc: 'Gene structures from GENCODE 21',
                       bwgURI: 'http://www.biodalliance.org/datasets/GRCh38/gencode.v21.annotation.bb',
                       stylesheet_uri: 'http://www.biodalliance.org/stylesheets/gencode2.xml',
                       collapseSuperGroups: true,
                       trixURI: 'http://www.biodalliance.org/datasets/GRCh38/gencode.v21.annotation.ix'}
   
                ]});
    
</script>

<div id="svgHolder"></div>

```


# Workflow

A common workflow loads... 

* a public reference genome (via DAS)
* a public gene annotation (via DAS)
* custom tracks with
    + quantitative data: `.bigbed`, `.bigwig` or indexed `.bam.`
    + or qualitative data: eg. `.gff` and `.vcf` (future) 

Where grouped tracks should be added in lists. In general, syntax to build a genome browser could resemble the [leaflet](https://rstudio.github.io/leaflet/) syntax to build maps.

```{}

dalliance %>% 
  addReference("GRCh38") %>% 
  addAnnotation("GENCODEv21") %>% 
  addTrack(list("my_track_A_rep1", "my_track_A_rep2"), 
            list("my_track_B_rep1", "my_track_B_rep2")) %>% 

```


