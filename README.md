
# RISIS-2018-course

# LEIDEN  RANKING versus RISIS PREDICTIONS
In this case-study, the goal is to predict  the  **[CWTS Leiden Ranking](http://www.leidenranking.com/)** using the university's  **characteristics** and **environment** from the **RISIS platform**. 

## Research Question
How to predict university ranks based on the university's characteristics and environment?

## Datasets of Interest
The goal here is to identify **potential datasets** that can be employed for successfully extracting the right data for analysis. 

#### University ranks
> The **Leiden Ranking** dataset contains ranking information on some major **worldwide universities**. This dataset can be use to test our hypothesis: **The university's characteristics and its organisations' dynamics determine its rank.**
> >**Dataset description**
> >The Leiden Ranking dataset offers **scientific performance indicators** of more than 900 major universities. These universities are only included when they are **above the threshold of 1000 fractionally counted Web of Science indexed core publications**. This explains its coverage across only **54 worldwide countries**.

#### Characteristics of the university
 > The **ETER** dataset provides **statistics** on **European Universities**. Although the dataset can not be used to test our hypothesis world wide, it can be used to test European universities. **Unfortunately**, the ETER dataset lacks information about types of organisation that surround a particular university.
 > >**Dataset description**
 >> The **E**uropean **T**ertiary **E**ducation **R**egister is a database on European Higher Education Institutions that not only includes **research universities**, but also **colleges** and a large number of **specialized schools**. The dataset covers **35 countries in 2015**.

#### Worldwide organisations
 > The **GRID** dataset on the other hand describes **Worldwide Organisations**. Using this data for example, we can **enrich ETER** with the number of (specific) organisations that surround a university and probably have some information on the dynamics of organisations around a university. **Unluckily**, neither ETER nor GRID define geographical boundaries.
 > >**Dataset description**
> > As of May 2018, the **G**lobal **R**esearch **I**dentifier **D**atabase describes 87868 organisations across 217 countries using 14220 relationships.  Only 17 countries (United States, United Kingdom, Japan, Germany, France, Canada, Czechia, China, India, Norway, Italy, Spain, Brazil, Russia, Switzerland, Sweden and Australia) within Grid host a thousand or more organisations. This accounts for 77% of the total. All organisations within Grid are assigned an address, while 96% of them have an organisation type (company, education, healthcare, non-profit, facility, government, archive, and 'other'), and only 80% have geographic coordinates. 
 
  #### Geographical boundaries
 > As the **GADM** dataset provides geographical boundaries and both ETER and GRID are described with coordinates, the GADM dataset can be used to **enrich ETER and GRID** with GADM level 2 geographical boundary code. The picture depicted below highlights the enrichment of the two datasets using GADM.
 > 
<img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/Enriched.png?raw=true" alt="IMAGE ALT TEXT HERE" width="1050" height="600" border="20"/>

 > >**Dataset description**
 > >The Database of **G**lobal **ADM**inistrative Areas, provides maps and spatial data for all countries and their sub-divisions,

## Datasets
Download the provided data from [here ](https://github.com/alkoudouss/RISIS-2018-course/blob/master/datasets.zip)

|Dataset  | Named Graph |
|:---------|:-------------|
| LEIDEN Ranking  | `http://risis.eu/dataset/leidenRanking_2015`| |
| ETER |  `http://risis.eu/dataset/eter_2014`  |
| ETER STATS enriched with GADM|  `http://risis.eu/dataset/eter_2014_enriched`|
| GRID [release of 2018-05-01](https://figshare.com/articles/GRID_release_2018-05-01/6216392)  | `http://risis.eu/dataset/grid_20180501` |
| GRID STATS enriched with GADM  | `http://risis.eu/dataset/grid_20180501_enriched` |
| GADM [released on 6 May 2018](https://gadm.org/data.html)  | - |


## Data Integration
The integration model depicted below highlights the use of the five datasets described earlier. 

<img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/IntegrationModel.png?raw=true" alt="IMAGE ALT TEXT HERE" width="1050" height="600" border="20"/>

## Integration Model: an implementation
The implemented integration data model depicted below describes a Lenticular Lens composed of **six linksets** and **two lenses** . 

 - **Linksets 1** and **2** are used to establish identity links between Leiden ranking and ETER based on either the **English** or **local** name of ETER's organisations on the one hand and on the other, based on the Leiden Ranking's **actors** using an exact string match algorithm. 
 - The same identity link discovery process is executed between ETER (**English** or **local** name) and GRID (**label** or **altLabel**) resulting in **linkset 2** and **3**. 
 - **Lens 1** enables putting together all links found between Leiden and ETER while **lens 2** does the same between ETER and GRID.  
 - We use **linkset 5** and **6** to restrict the links to those for which a geographical boundary is found in GADM.
 
<img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/IntegrationModel-2.png?raw=true" alt="IMAGE ALT TEXT HERE" width="1050" height="600" border="20"/>

## Hands-on sessions
1. Introduction to the Lenticular Lens Tool
2. Converting ETER from **csv** to **RDF** 
3. Load all datasets (either with the **LL tool** or the **Stardog** triple store)
4. Load the provided research question 
5. Using the Lenticukar Lens Tool

# Using the LL
How did the name came about?
## Main menu

- `MODE: CREATION/ADMIN` Use this to switch between creation and admin modes
 - `STARDOG ON/OFF` Use this to turn on/off the Stardog TripleStore

>### Creation Mode
> + `RESEARCH QUESTION` Create and manage research questions
> + `RESOURCE CLUSTER` Create and manage resource clusters meant for grouping resources based on a certain criteria before creating a linkset (under development)
> + `LINNKSET FROM CLUSTER` Create and manage linksets from resource clusters (under development)
> + `LINKSET` Create and manage linksets
> + `LENS` Create and manage lenses as combination of already created linksets
> + `VIEW` Create and manage views over the datasets based on the created alignments (linksets/lenses)
> + `LINK CLUSTER` Create clusters to analyse the resulting alignments (linksets/lenses). Also allow for inspecting datasets properties and values and to enrich dataset with geodata from a given endpoint (under development)
> + `IMPORT` Import (i) csv-files into RDF datasets, (ii) external linksets (created by another tool) and (iii) research questions

> ### Admin Mode
> + `TRIPLESTORE` Offers some of the *stardog* admin options, as well as pre-defined queries
> + `RESEARCH QUESTIONS` Delete a selected research question
> + `DEL LINKSETS`  Delete *all* linksets from the database
> + `DEL LENSES` Delete *all* lenses from the database
> + `DEL VIEWS` Delete *all* views from the database
	
## The `RESEARCH QUESTION` main menu
Using the tool starts with creating a research question  as all alignment activities are documented in a research question. 

> ### Research Question sub-menu
> After clicking on the `RESEARCH QUESTION` button from the main menu, the following options are available:
>+ The `INSPECT` button displays on the left side **all available dataset in the system** and on the right side all the **selected datasets** for the selected research question.
>+  The `CREATE` button prompts you with a div for inserting the description of a research question as a first step to create a research question. <a href="https://www.youtube.com/watch?v=CcffBlCBF54&index=6&list=PLo4YbUaRFSnwJ9XJvp6rlIMsaw_rfKT9C"><img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/play.png?raw=true" alt="IMAGE ALT TEXT HERE" width="30" height="15" border="10" /></a>
>+ The `EXPORT` button enables **exporting the selected research question and all its alignments and views**. 
>+ The `OVERVIEW` button displays all activities performed within the selected research question.  

## The `LINKSET` main menu
The linkset menu manages everything dealing with linkset.

> ### Linkset sub-menu
> After clicking on the `LINKSET` button from the main menu, the following options are available:
>+ The `INSPECT` button **displays all linksets** in the research question.
>+  The `CREATE` button prompts you with a div for inserting the linkset's specifications in order to create a context specific linkset. <a href="https://www.youtube.com/watch?v=rF4m2A0-U0U&list=PLo4YbUaRFSnwJ9XJvp6rlIMsaw_rfKT9C&index=3"><img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/play.png?raw=true" alt="IMAGE ALT TEXT HERE" width="30" height="15" border="10" /></a> (see available methods bellow)
>+ The `EDIT` button enables **editing a linkset's label** or **deleting a linkset**.
>+ The `REFINE` button enables **refining a linkset**.
>+ The `EXPORT` button enables **exporting an linkset** by selecting from the options '`Flat | Flat + Metadata | All`.  (the `Plot` option is of no relevance to the user at present). 
>+ The `IMPORT` button enables the user to **directly imported** a linkset already created for another research question.  
	
 >#### Methods for creating a Linkset
>Linksets can be created by clicking the **LINKSET** button or  the **LINKSET FROM CLUSTER** button from the main menu. Once a linkset is created, it can be refined based on new identity criteria (constraints). The list below highlight the available algorithms for link discovery.
>+ String similarity by **exact match** , **approximate match**   or **mapping via intermediate dataset**
>+ URL Identifier
>+ Geographical similarity
>+ Number approximation 
>+  Embedded alignment	
>
>When creating a linkset the LL tool checks whether the linkset already exists using the linkset specifications provided by the user. If the linkset already exists, it is not be created but it is  **imported** instead. 
		
## The  `Lens` main menu


The lens menu manages everything dealing with lens.

> ### Lens sub-menu
> After clicking on the `LENS` button from the main menu, the following options are available:
>+ The `INSPECT` button **displays all lenses** in the research question.
>+  The `CREATE` button prompts you with a div for inserting the  lens' specifications in order to create a context specific lens. <a href="https://www.youtube.com/watch?v=_rV9k9RPbAs&list=PLo4YbUaRFSnwJ9XJvp6rlIMsaw_rfKT9C&index=4"><img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/play.png?raw=true" alt="IMAGE ALT TEXT HERE" width="30" height="15" border="10" /></a> (see available methods bellow)
>+ The `EDIT` button enables **editing a lens' label** or **deleting a lens**.
>+ The `REFINE` button enables **refining a lens**.
>+ The `EXPORT` button enables **exporting an lens** by selecting from the options '`Flat | Flat + Metadata | All`.  (the `Plot` option is of no relevance to the user at present). 
>+ The `IMPORT` button enables the user to **directly imported** a lens already created for another research question.  
	
 >#### Methods for creating a Lens
> Lens can be created by clicking the **LENS** button from the main menu. Once a lens is created, it can be refined based on new identity criteria (constraints). The list below highlight the available algorithms for creating a lens.
>+ Union
>+ Intersection (under development)
>+ Transitive
>+ Difference

>When creating a lens the LL tool checks whether the lens already exists using the lens specifications provided by the user. If the lens already exists, it is not be created but it is  **imported** instead. 
>
>In order to refine a lens, it has to be composed of linksets of the same **target** and **source** datasets. 


## The `View` main menu

The View menu manages everything dealing with view. It also provides user with extracting the data of interest for analysis based on the an implemented integration model.

> ### View sub-menu
> After clicking on the `VIEW` button from the main menu, the following options are available:
>+ The `INSPECT` button **displays all views** in the research question.
>+  The `CREATE` button prompts you with a div for inserting the  view's specifications in order to create a context specific view. <a href="https://www.youtube.com/watch?v=2Ihs5j1kmZU&list=PLo4YbUaRFSnwJ9XJvp6rlIMsaw_rfKT9C&index=5"><img src="https://github.com/alkoudouss/RISIS-2018-course/blob/master/Images/play.png?raw=true" alt="IMAGE ALT TEXT HERE" width="30" height="15" border="10" /></a> 
>+ The `EDIT` button enables **editing a view's label** or **deleting a view**.

## Validation
### Link based validation
### Cluster based validation (under development)


## GRID STAT enrichment with GADM example
```
#### Query for enriching GRID with organisation counts at GADM level-2
PREFIX dataset:		<http://risis.eu/dataset/>
prefix foaf: 		<http://xmlns.com/foaf/0.1/>
prefix grivocab: 	<http://www.grid.ac/ontology/>
prefix ll: 			<http://risis.eu/alignment/predicate/>
PREFIX gadm: 		<http://geo.risis.eu/vocabulary/gadm/>
PREFIX coord:		<http://www.w3.org/2003/01/geo/wgs84_pos#>

INSERT
{
  GRAPH dataset:grid_20170712_enriched
  {
  	?grid a				?type ;
    	  ll:level 		2 ;
          ll:typeCount	?count .
  }
}

WHERE
#SELECT *
{
	{
		SELECT ?country ?city ?type ?level (count(?type) as ?count)
		{
			# ENRICHED DATASET
			GRAPH dataset:grid_20170712_enriched 
			{
			  ?grid ll:intersects ?gadm .
			}	
			# GRID INSTANCE DATA 
			GRAPH dataset:grid_20170712
            {
              ?grid rdfs:label				?name ;
                    a						?type ;
                    a						foaf:Organization ;
                    grivocab:hasAddress 	?address .
              ?address grivocab:cityName 	?city ;
                    grivocab:countryName 	?country ;
                    coord:lat				?lat ;
                    coord:long				?long .
            } 
		} group by ?country ?city ?level ?type order by ?country ?city ?level ?type
	}

	# GRID INSTANCE DATA 
	GRAPH dataset:grid_20170712
	{
	  ?grid rdfs:label				?name ;
			a						?type ;
			a						foaf:Organization ;
			grivocab:hasAddress 	?address .
	  ?address grivocab:cityName 	?city ;
			grivocab:countryName 	?country ;
			coord:lat				?lat ;
			coord:long				?lon .
	}  
}
```
## CREATION OF GRID NETHERLANDS
```
INSERT {
	graph <http://risis.eu/dataset/grid_20180501_NL>
    {
      	?sub	?pred0	?obj0.
    	?sub	?pred1 	?obj1.
      	?obj1	?pred2	?obj2. 
    }
}

#select distinct  *
WHERE
{
  
  	graph <http://risis.eu/dataset/grid_20180501>
    {
      	?sub	?pred0	?obj0.
    	?sub	?pred1 	?obj1.
      	?obj1	?pred2	?obj2. 
    }
          
	graph <http://risis.eu/dataset/grid_20180501>
    {
    	?sub  <http://www.grid.ac/ontology/hasAddress>/<http://www.grid.ac/ontology/countryCode> ?countryCode.
      	filter (?countryCode = "NL")
    }
    
} 
```

## EXPORT OF GRID NETHERLANDS
```
CONSTRUCT 
{
	graph <http://risis.eu/dataset/grid_20180501_NL>
    {
      	?sub	?pred0	?obj0. 
    }
}
{
	graph <http://risis.eu/dataset/grid_20180501_NL>
    {
      	?sub	?pred0	?obj0. 
    }
}
```