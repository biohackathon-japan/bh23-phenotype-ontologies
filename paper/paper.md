---
title: 'BioHackJP 2023 Report R1:Improving phenotype ontology interoperability
'
title_short: 'BioHackJP 2023 Improving phenotype ontology interoperability'
tags:
  - ontology
  - Large Language Models
authors:
  - name: Eisuke Dohi
    orcid: 0000-0002-5365-4900
    affiliation: 1
  - name: Tatsuya Kushida
    orcid: 0000-0002-0784-4113
    affilication: 2
  - name: Yuki Yamagata
    orcid: 0000-0002-9673-1283
    affilication: 2
  - name: Terue Takatsuki
    orcid: 0000-0003-0011-764X
    affilication: 3
  - name: Jaemoon Shin
    orcid: 0000-0001-5859-601X
    affilication: 3
  - name: Hiroshi Masuya
    orcid: 0000-0002-3392-466X
    affilication: 2
  - name: Thomas Liener
    orcid: 0000-0003-3257-9937
    affilication: 4
  - name: Robert Hoehndorf
    orcid: 0000-0001-8149-5890
    affiliation: 5
affiliations:
  - name: National Center of Neurology and Psychiatry, National Institute of Neuroscience, Japan
    index: 1
  - name: RIKEN BioResource Research Center, Japan
    index: 2
  - name: Database Center for Life Science ROIS-DS, Kashiwa, Chiba, Japan
    index: 3
  - name: Unaffiliated
    index: 4
  - name: King Abdullah University of Science and Technology, Saudi Arabia
    index: 5
date: 30 June 2023
cito-bibliography: paper.bib
event: BH23JP
biohackathon_name: "BioHackathon Japan 2023"
biohackathon_url:   "https://2023.biohackathon.org/"
biohackathon_location: "Kagawa, Japan, 2023"
group: R1
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/biohackathon-jp/bh23-report-template
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Dohi \emph{et al.}
---

# Background

Ontologies play a crucial role in data management and especially in life science, they have been indispensable for decades as the complexity of life science data requires rigor. Biomedical ontologies often undergo change and improvement, as e.g. disease and phenotype ontologies develop constantly along with our scientific understanding. In order to bridge the gap between ontologies and annotated datasets and thus to semantically enable applications and datasets to retrieve insights and improve interoperability, ontology mapping plays a key role [1]. 

For example, as a role for search function interface, an ontology is used to absorb fluctuations in expression due to synonyms and to guide users through generalization/specialization. Links as rdfs:subClassOf, thereby contributing to clarifying users' interests and indicating users' desired search results. The use of links between terms may also be used to meet the needs of users across domains. For example, modern life sciences are strongly expected to contribute to medical science, but the phenotypic vocabulary used for many model organisms is different from that used in medical science. Mapping data between Human Phenotype Ontology (HPO) [2, 10] and phenotypic ontologies of each model organism research field has been implemented in many databases to meet the needs of searches across research fields [3, 4, 5]. 

In addition to data searching, a bird's-eye understanding of the data set is important for scientists. Users not only want detailed information on individual pieces of information, they also want to know where their interest targets within their own research area. The need for good overview and easy understanding of the overall and partial structure of the data for clinicians and biologists working in a variety of fields is also a major challenge that cannot be ignored. Depending on the domain and site of use, synonyms and definitions can vary which would not be noticed without communication with the end users. Ontology can help understanding the domain’s knowledge by providing vocabularies or terms with their classification and relationships.
 
To implement a sophisticated search supported by semantics, interoperability to address cross-disciplinary needs is crucial. In this paper we focus on different aspects of interoperability of ontologies, especially in the phenotype and disease domain and how they could be improved: 

One aspect is not technical but linguistic and social interoperability - improving the usage and understanding of datasets through translation of ontologies into other languages like Japanese. While this might not seem challenging at first from a scientific or mathematical perspective, it is actually a very challenging task as translations in general might introduce unacceptable fuzziness: An exact translation can be viewed similarly strict as a skos:exactMatch statement in ontology matching - but sometimes such an exact translation is not possible, especially for languages from different  families, e.g. Indo-Germanic, Japanese or Arabic. [Please see Background translations for more details on translation]   

Another aspect of this paper is the interoperability between the HPO and Mammalian Phenotype Ontology (MP) [ 7] on a technical and structural level. MP is a phenotype ontology provided by MGI [11]. These ontologies are very important to harmonise human data and model animal data, e.g., to maximise the outcome  from previous experiments with model organisms to minimise the sacrifice of animals. Ontology mapping  [see Background mappings] is a hard problem in general and especially in the case of HPO  and MP challenging  [see Outcome/other chapters LLM/ Gene expression/etc]. 

Because of this multifaceted nature of the problem, a multidisciplinary hackathon that includes not only linguists and informaticians, but also clinicians and life scientists, who are the most end-users, will provide an excellent opportunity to share current awareness and identify challenges for the future. During the BioHackJP 2023, a variety of approaches were discussed and evaluated. Focusing on the interoperability of the translation and mapping of ontologies, we discussed the following six issues:
 
1) Ontology translation to Japanese - current status and issues
2) Translation issue 2 - mappings between English and Japanese
3) HP-MP interoperability 1 - Differences of categorical layer dependent on view points
4) HP-MP interoperability 2 - definition analysis with LLM 
5) HP-MP interoperability 3 - LLM based Alignment workflow suggestions for axioms, labels and definitions
6) HP-MP interoperability 4 - Exploration of model mice relevant to human phenotypes and diseases


In this paper, we report overviews of the result of each investigation. And discussed future works to be addressed regarding these challenges.


# Outcomes

To achieve our objectives, we conducted a comprehensive survey of open source language models available and evaluated their suitability for our task. We explored different models, taking into consideration factors such as performance, computational requirements, and ease of deployment. Subsequently, we sought to run the selected models on a local computer, ensuring that the infrastructure requirements were met.

Having established a working environment for LLMs, we developed a set of pipelines that incorporated various natural language processing techniques to extract relevant biological terms from textual data. These terms were then matched and mapped to the corresponding ontology terms, thereby providing a standardized representation of the extracted information. By utilizing Linked Data principles, we aimed to create an interconnected network of biological knowledge that would facilitate data integration and enable advanced analysis.

![Caption for BioHackrXiv logo figure](./biohackrxiv.png)

# Future work

In this paper, we examine six critical issues related to ontology interoperability, translation to multiple languages, and the relationships among terms across diverse ontologies. These issues were probed during an international hackathon that assembled a varied set of researchers from distinct life science communities. Our findings underscore the interconnectedness of these issues and suggest that they require a comprehensive solution. One recommendation posits the need to redesign the hierarchical structure of ontologies. This restructuring aims to standardize translations across ontologies, establish accurate term relationships, and facilitate a high-level understanding of the ontology.  How to organize the layer is a big challenge, however, this is one of the fundamental problems exist in the every ontology. To address these issues we need to combine several methods including the compression of layers with terms based on the concept or newly annotated tag etc. 

We also observed the necessity for multi-dimensional improvements in interoperability that can transcend various domains such as species, disciplines, and both human-computer and computer-computer interactions. Although many software applications have adopted ontology visualization based on rdfs:subClassOf links, this approach is often inadequate for biomedical researchers. The field of ontology research acknowledges that human understanding varies across different categorical layers, influenced by perspective and context. Despite existing research on dynamic data structures and methodologies, the biomedical sector still lacks extensive, user-friendly ontology tools. Therefore, the development of intuitive visualization software, along with the refinement of ontology knowledge structures, is imperative.


To address these challenges, we advocate for the development of next-generation ontologies that incorporate machine learning and language models. These advanced systems could offer flexible, specialized information while maintaining a comprehensive and holistic view of the knowledge base.

The utilization of Lexical Language Models (LLMs) is a forthcoming imperative task. Specifically, the integration of lexical and semantic (axiom) components in mapping strategies could be beneficial. As a part of our quantitative evaluation, we intend to measure 'ChatGPT distance' to assess semantic similarity, combining natural language and logical definitions, such as EQ models in ontologies. This evaluation will contribute to the effectiveness of the existing HPO-MP mapping data, currently used for research on mice and other model organisms relevant to human phenotypes and diseases. It will also facilitate the alignment of various ontologies and the application of new mappings for disease modeling and gene-disease associations. Moreover, an exploration of the relationships among translations, axioms, and LLM embeddings may enhance coordination between phenotype ontology developers, software engineers, and end-users in biomedical science.
In conclusion, the hackathon reaffirmed that interdisciplinary collaborations could offer diverse perspectives on a problem, thereby facilitating more comprehensive solutions. Technological advancements in this domain, including the use of LLMs, are promising and likely to provide innovative solutions to the challenges discussed herein.  The next Hackathon will continue to serve as platforms for discussing these complex issues and identifying potential solutions.


## Acknowledgements

We would like to thank the fellow participants at BioHackathon 2023 for their collaboration and constructive advice, which greatly influenced our project. We are grateful to the organizers for providing this platform and the developers of open source language models. Special thanks to our mentors, advisors, and colleagues for their guidance and support. Without their contributions, our project in linked data standardization with LLMs in bioinformatics would not have been possible.

## References

1, Ian Harrow, Rama Balakrishnan, Ernesto Jimenez-Ruiz, Simon Jupp, Jane Lomax, Jane Reed, Martin Romacker, Christian Senger, Andrea Splendiani, Jabe Wilson, Peter Woollard
Ontology mapping for semantically enabled applications
Drug Discovery Today Volume 24, Issue 10, October 2019, Pages 2068-2075
DOI: https://doi.org/10.1016/j.drudis.2019.05.020

2, Kohler S, Carmody L, Vasilevsky N, Jacobsen JO, Danis D, Gourdine JP, et al. Expansion of the Human Phenotype Ontology (HPO) knowledge base and resources. 
Nucleic Acids Res 2018;47:D1018–D1027.
DOI: https://doi.org/10.1093/nar/gky1105

3, Masuya H, Usuda D, Nakata H, Yuhara N, Kurihara K, Namiki Y, Iwase S, Takada T, Tanaka N, Suzuki K, Yamagata Y, Kobayashi N, Yoshiki A, Kushida T.
Establishment and application of information resource of mutant mice in RIKEN BioResource Research Center.
Lab Anim Res. 2021 Jan 18;37(1):6. 
DOI: https://doi.org /10.1186/s42826-020-00068-8

4, BioResource MetaDatabase: https://knowledge.brc.riken.jp/ 

5, HPO-MP RDF data: https://github.com/kushidat/outcomes_BH23/blob/main/Data/hp_mp_mapping.ttl 

6, HPO annotation data: https://data.monarchinitiative.org/monarch-kg-dev/2023-06-01/rdf/index.html#:~:text=hpoa_disease_phenotype.nt.gz

7, Smith CL, Eppig JT. 
The mammalian phenotype ontology: enabling robust annotation and comparative analysis. Wiley Interdiscip Rev Syst Biol Med. 2009 Nov-Dec;1(3):390-399. doi: 10.1002/wsbm.44. PubMed PMID: 20052305; PubMed Central PMCID: PMC2801442.

8, Kota Ninomiya, Terue Takatsuki, Tatsuya Kushida, Yasunori Yamamoto, Soichi Ogishima
Choosing preferable labels for the Japanese translation of the Human Phenotype Ontology
Genomics & Informatics 2020; 18(2): e23.
Published online: June 18, 2020
DOI: https://doi.org/10.5808/GI.2020.18.2.e23

9, Nicolas Matentzoglu, James P Balhoff, Susan M Bello, Chris Bizon, Matthew Brush, Tiffany J Callahan, Christopher G Chute, William D Duncan, Chris T Evelo, Davera Gabriel, John Graybeal, Alasdair Gray, Benjamin M Gyori, Melissa Haendel, Henriette Harmse, Nomi L Harris, Ian Harrow, Harshad B Hegde, Amelia L Hoyt, Charles T Hoyt, Dazhi Jiao, Ernesto Jiménez-Ruiz, Simon Jupp, Hyeongsik Kim, Sebastian Koehler, Thomas Liener, Qinqin Long, James Malone, James A McLaughlin, Julie A McMurry, Sierra Moxon, Monica C Munoz-Torres, David Osumi-Sutherland, James A Overton, Bjoern Peters, Tim Putman, Núria Queralt-Rosinach, Kent Shefchek, Harold Solbrig, Anne Thessen, Tania Tudorache, Nicole Vasilevsky, Alex H Wagner, Christopher J Mungall
A Simple Standard for Sharing Ontological Mappings (SSSOM) 
Database, Volume 2022, 2022, baac035
DOI: https://doi.org/10.1093/database/baac035

10, Matthias Griese, Matthias Haimel, Julia Pazmandi, Marc Hanauer, Nomi L Harris, Michael J Hartnett, Maximilian Hastreiter, Fabian Hauck, Yongqun He, Tim Jeske, Hugh Kearney, Gerhard Kindle, Christoph Klein, Katrin Knoflach, Roland Krause, David Lagorce, Julie A McMurry, Jillian A Miller, Monica C Munoz-Torres, Rebecca L Peters, Christina K Rapp, Ana M Rath, Shahmir A Rind, Avi Z Rosenberg, Michael M Segal, Markus G Seidel, Damian Smedley, Tomer Talmy, Yarlalu Thomas, Samuel A Wiafe, Julie Xian, Zafer Yüksel, Ingo Helbig, Christopher J Mungall, Melissa A Haendel, Peter N Robinson
The Human Phenotype Ontology in 2021
Nucleic Acids Research, Volume 49, Issue D1, 8 January 2021, Pages D1207–D1217 
DOI: https://doi.org/10.1093/nar/gkaa1043

11, Mouse Genome Informatics: https://www.informatics.jax.org/index.shtml

12, uPheno: https://obophenotype.github.io/upheno/

13, HoIP: https://bioportal.bioontology.org/ontologies/HOIP

14, Yuki Yamagata, Tsubasa Fukuyama, Shuichi Onami, Hiroshi Masuya
Ontology for Cellular Senescence Mechanisms
bioRxiv 2023.03.09.531883
DOI: https://doi.org/10.1101/2023.03.09.531883

15, Kushida T, Mendes de Farias T, Sima AC, Dessimoz C, Chiba H, Bastian F, Masuya H. Exploring Disease Model Mouse Using Knowledge Graphs: Combining Gene Expression, Orthology, and Disease Datasets. 
bioRxiv 2023.08.30.555283
DOI: https://doi.org/10.1101/2023.08.30.555283

16, BioResource MetaDatabase: https://knowledge.brc.riken.jp/ 

17, HP-MP RDF data: https://github.com/kushidat/outcomes_BH23/blob/main/Data/hp_mp_mapping.ttl 

18, HPO annotation data: https://data.monarchinitiative.org/monarch-kg-dev/2023-06-01/rdf/index.html#:~:text=hpoa_disease_phenotype.nt.gz 

19, SPARQL query for the integrated bioresource KG: https://github.com/kushidat/outcomes_BH23/blob/main/QueryExample/bh23_sparal_querty_example01.txt 

20, Bioresource SPARQL endpoint: https://knowledge.brc.riken.jp/sparql 


## Supplemental data

Supplemental data 1: Collected HP-MP mapping data including ZP, and WBP. They include 14,902 HP-MP mapping data in total.
uPheno2 [HP-MP]: http://obofoundry.org/ontology/upheno.html 
mp_hp-align equiv [HP-MP]: https://github.com/obophenotype/upheno/blob/master/hp-mp/mp_hp-align-equiv.owl 
Mapping commons (mh_mapping_initiative) [HP-MP]: https://github.com/mapping-commons/mh_mapping_initiative 
HP-MP SSSOM [HP-MP]: https://github.com/mapping-commons/sssom 
uPheno [HP-MP, HP-ZP, and HP-WBP]: https://github.com/obophenotype/upheno 

Supplemental data 2: Overview of the HP-MP mapping data (excluded uPheno data): https://github.com/kushidat/outcomes_BH23/blob/main/Figure/Overview_of_HP-MP_mapping_data.png 

Supplemental data 3: Phenotypic data between model organism and human: https://github.com/kushidat/outcomes_BH23/blob/main/Figure/phenotypic_data_between_model_organism_and_human.png 

