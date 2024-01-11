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
2) Improving ontology alignments and mappings
3) HP-MP interoperability 1 - Differences of categorical layer dependent on view points
4) HP-MP interoperability 2 - definition analysis with LLM 
5) HP-MP interoperability 3 - LLM based Alignment workflow suggestions for axioms, labels and definitions
6) HP-MP interoperability 4 - Exploration of model mice relevant to human phenotypes and diseases


In this paper, we report overviews of the result of each investigation. And discussed future works to be addressed regarding these challenges.


# Ontology translation to Japanese - current status and issues 

## Background
Since March 2023, the Database Center for Life Science (DBCLS) has provided a Japanese version of the Mammalian Phenotype Ontology (MP), which can be accessed at https://github.com/dbcls/MP_Japanese. 
The translation of MP into Japanese serves several crucial purposes. It accelerates the phenotypic annotation of genomic data within Japan, fosters international (re)use of phenotypic annotations generated by Japanese researchers, facilitates Japanese researchers in readily (re)using internationally annotated phenotypic annotations, and contributes to the broader field of mammalian research. The translation process involved initial machine translation, followed by meticulous manual curation. Furthermore, experts were engaged to oversee the incorporation of genetics and medical terminology.
However, during the translation process, a number of issues became clear when translating into Japanese. It has become clear that these problems depend on the characteristics of each language when becoming multilingual.

## Outcomes
Ontologies rely on precision and correctness and thus translating languages as distant as English and Japanese, can be very challenging. Japanese has multiple types of characters, kana summarizes the character set hiragana and katakana – both represent the same sounds and so one could think to use them interchangeably, but that is wrong. The context matters in order to recognize the symbol correctly. For example, the symbol "癌" will be understand as cancer, but "ガン" might be recognize as a gun or a kinds of bird.  Kanji characters are different as they do not represent syllables but concrete word or concepts. Therefore there are many thousands characters in kanji, which have to be memorized. 

Also within a character set, context is important. For example, while the word ‘male’ is used in English to describe the sex of both, mammals and humans, this is not the case in Japanese. In mammals "雄”is used for ‘male’, but in humans it is "男".   

Naturally, the complexity of the Japanese language hinted at above poses problems to automatic machine translation. Tools like Google Translate and DeepL are used to support the translation efforts, however – manual curation is needed to ensure highest quality.  See figure 1 for the proposed workflow to translate HPO and MP from English to Japanese.   

![Fig1](./Fig1.jpg)
Figure 1: Proposed workflow for HPO/MP translation, taken from “Choosing preferable labels for the Japanese translation of the Human Phenotype Ontology” [8] 


# Improving ontology alignments and mappings

To align ontologies and to find mappings between ontologies is a well described and relevant problem to boost interoperability, however it is still very challenging. The definition of “mapping” or “match” is often interpreted very differently by different people. Strictly speaking, an “exact match” means that two concepts can be used interchangeably. To describe other types of relationships, other properties could be used like skos:broader, skos:narrower or skos:related - to determine the exact type of a mapping can be very challenging automatically and usually, to create a “gold standard”, manual curation and manual quality control of domain experts is needed.   

To capture mappings and their provenance in a standardised way, recently A Simple Standard for Sharing Ontological Mappings(SSSOM), a common standard for sharing ontological mappings was proposed [9] [cite https://doi.org/10.1093/database/baac035]. 

During the biohackathon SSSOM was discussed and proposed as a way to share ontological mappings that might be created in the future. Further, different methods to investigate and potentially improve ontology alignment and thus interoperability in the future were discussed and are presented here. The focus for these analyses are the ontologies HPO and MP.

# HP-MP interoperability 1 - Differences of categorical layer Odependent on view points

## Background
Here, we examined how HPO and MPO are perceived by the end-users, who are closest to the field, from a structural point of view, referring to the opinions of medical researchers who have many years of experience in behavioural studies using mice as well as clinicians. At first, we attempted to examine whether there are differences in the structure of the ontology between HPO and MPO. To address this, we extracted terms in each layer with SPARQL endpoints to analyse the structure of HPO and MPO, and features between each step between the layers. We raised fundamental structural problems within individual ontologies and between ontologies according to the observation.
① Category：In the 1st layer, most highest concepts were listed based on anatomy, systems and time-points etc. We found that even in the 1st layer there are 6 differences between HPO and MPO after manual mapping. Among the 6 different terms, one was only in HPO (constitutional symptoms) and there were in MPO (normal phenotype, mortality/aging, no phenotypic analysis). Some of the higher concepts were divided into lower concepts in HPO but not in MPO. 
② Step：The number of layers and the numbers of terms in each layer will be dependent on the complexities of anatomy, systems and time-points etc. For example, the number of terms in 8th layer, HPO is 4877 but MPO is 2394, showing substantial differences between ontologies. In addition to the complexities of categories, the meaning and rationale of the branching to the lower concepts are not consistent each time. 
③ Granularity：When the above two issues are stacked together, the endo-phenotype at the same granularity is placed on different layers within ontology and between ontologies, making it impossible to visualise the terms of the same granularity on the same layer, leading to intuitive understanding. This makes it difficult for clinicians and researchers using model animals to understand and overview the ontology.

## Outcomes
This observation reveals that there are many structural ambiguities. This lack of a bird's eye view of the ontology, which exists in most ontologies, is a major barrier to collaboration with experts with in-depth domain knowledge to improve the ontology for the field and to modify, add, or delete words. This will be an important issue for further mapping and collaborative validation. At the same time, however, those also suggest that there may be many areas that remain to be improved. Following are some of the ideas that come up based on the above mentioned observations.
1: Mapping between ontologies only with the key upper concepts：The main usage of mapped ontology in inter-species is the phenotype translation of human and model organisms. After the phenotype translation, researchers will move on to analyse more detail in model organisms. Since perfect ontology mapping is impossible in an inter-species manner, this would be one of the alternatives for usage. But even in this choice, granularity of terms needs to be aligned. 
2: Layer alignment for end-phenotypes：The end-phenotypes are the detailed descriptions of phenomes, so layer alignment of these terms with compression of layers based on concepts would be helpful. However, this also requires detailed understanding of each term in the context of categories and branching.
Above two may be possible, if the ontology structure can be transformed flexibly and freely. But this may require assigning meaning to terms and branches. Not only for the mapping, organising the layer in terms of inter-species manner will help for understanding and improvement for visibility. These problems might also exist in other ontology and how to deal with these fundamental problems would be helpful to map with other model organisms.


# HPO-MP interoperability 2 - definition analysis with LLM

## Background
Large Language Models (LLMs) such as LLaMA and GPT have demonstrated that they are able to capture the meaning of natural language expression. We used LLMs to generate embeddings of the definitions of classes in HPO and MP, and then used the generated embeddings to determine whether the definitions are semantically similar; to determine semantic similarity, we compared the embeddings of the definitions using a vector similarity measure. This approach can be used for matching classes from HPO and MP by computing the pairwise similarity between them, and then, for each class from one ontology, rank all classes from the other ontology; we can evaluate this approach by determining where correctly matching classes (if any) are ranked.

## Outcomes
We implemented a sentence embedding model using the Python transformers library based on the bert-base-uncased pre-trained model. We obtained all definitions for classes from HPO and MP and generated a phrase-level embedding; to achieve this goal, we used the transformer to generate an embedding for each word and then aggregated the embeddings using the mean aggregation to generate the phrase embedding. To determine similarity, we used both cosine similarity and the Euclidean distance.
Fig. 2 shows a TSNE for the generated embeddings. As can be seen in the figure, there is a relatively strong separation between MP and HPO definitions, demonstrating that they are different and not recognized as very similar. One of the reasons for this separation may be that MP definitions are often substantially shorter and may not always be formulated as a full sentence, whereas definitions in HPO are full sentences and may even span multiple sentences. 
Figure 2. TSNE visualization of the embeddings generated from definitions in HPO and MP. Embeddings derived from MP are shown in blue, from HPO in red.
Github Link: https://github.com/leechuck/biohack23 

# HP-MP interoperability 3 - LLM based Alignment workflow suggestions for axioms, labels, and definitions for HPO and MP

## Background
The challenge in cross-species phenotypic mapping and alignment is handling species-specific differences. In order to overcome difficulties, it is necessary to consider semantic similarity beyond mere label matching. This study investigated whether Large Language Models (LLMs) support cross-species phenotypic ontology alignment toward interoperability between phenotype and disease. We used ChatGPT / GPT-4 and explored the performance to compare HPO and MP ontologies.

## Outcomes
1.	Ontology alignment evaluation  
First, if no ontology information was not given, such as definitions or subclasses, ChatGPT made comparative evaluations based on label matches. In addition, asking ChatGPT to consider the semantic similarity, the evaluation scores varied widely over three trials since the evaluation was based on pre-trained general knowledge independent of domain-specific ontologies. Next, in addition to the labels, we gave the information on the definitions in each ontology using annotation properties in OWL. As a result, comparative evaluation was possible regarding their semantic similarity. Furthermore, logic-based evaluation was possible using owl:equivalentClass, even if their labels were different. For example, whereas MP:0002544 brachydactyly has a different label than HP:11927 Short digit, GPT-4 rated their similarity scores as high since their owl:equivalentClass axioms show both of which have part ‘decreased length’ and inhere in ‘digit’  described in the same Entity-Quality (EQ) manner.

In summary, ChatGPT/GPT-4 can be applied to evaluating ontology alignment. Whereas AI hallucinations are problems, prompt learning using logical definitions of ontology will contribute to helping reduce risks and be more cost-effective than fine-tuning. 


2. Towards alignment with consideration of disease interoperability
The differences in granularity between HPO and MP hierarchies cause difficulties in ontology alignment. For example, HPO HP:001156 Brachydactyly has more rich subclasses of some distinct patterns of shortened digits (brachydactyly types A-E) dependent on disease classification. Therefore, developing a core reference ontology from general to species-specific layers is desirable concerning ontology alignment. Unified phenotype ontology (uPheno) [12] is a good candidate ontology. However, uPheno includes a large number of entities based on structural or morphological perspectives, such as ‘abnormal blood vessel morphology’ (UPHENO_0020584), ‘abnormal artery morphology’ (UPHENO: 0019771), and ‘abnormal systemic artery morphology’ (UPHENO: 0020587). Such entities lead to multiple inheritances, which cannot help us understand the inherent phenotypes nor help us find associations of diseases. As subclasses of general phenotypes from PATO, we need a reference ontology having hierarchical sub-trees with single inheritance, for example, ‘constricted (PATO: 0001847),’ ‘vascular stenosis,’ ‘arterial stenosis,’ and ‘coronary stenosis　(Fig. 3).

Figure 3.　Ontology alignment with multiple ontologies and biomedical terminologies. PATO hierarchy is green, HPO hierarchy is right blue, MP is green, uPheno is pink, MeSH is yellow, DOID is orange, and the desirable reference ontology is blue.  
Homeostasis Imbalance Process ontology (HoIP) [13, 14] consists of three layers: domain-independent layer, biomedical dependent layer, and homeostasis imbalance-dependent layer, and utilizes PATO, HPO, the anatomy ontology UBERON, the Symptom Ontology, the disease ontology DOID in the biomedical dependent layer described by OWL-DL. Therefore, the HoIP schema may contribute to ontology alignment.　HoIP is based on manual annotation, which is costly; if the LLM can handle complex knowledge by working with the ontology and dynamically learning interpretations of various information, both the ontology and the LLM can amplify knowledge with each other, generating a transparent and robust knowledge base.

# HP-MP interoperability 4 - Exploration of model mice relevant to human phenotypes and diseasesO

## Background

RIKEN BioResource Research Center (BRC) is constructing a bioresource knowledge graph (KG) [15]. The users can explore their bioresources (e.g., RIKEN BRC mice relevant to specific MP terms.) for the KG. Leveraging human phenotype and disease information, we aimed to expand the information on model mice expected to be used for health care and medical research.　　　
We collected external public data, integrated these data with the bioresource KG in the triple store: BioResource MetaDatabase, and executed a SPARQL query to explore model mice as follows.
Collecting the existing HPO-MP mapping data (see Supplemental data 1, 2)
Generating the HPO-MP RDF data from the HPO-MP mapping data.
Integrating the Bioresource KG with the HPO-MP RDF data and HPO annotation data within Monarch KG (Fig.4).
Executing a SPARQL query for the integrated bioresource KG to explore model mice relevant to human phenotype and diseases on the Bioresource SPARQL endpoint.

## Outcomes
We obtained 1875 mice relevant to 8834 HPO terms and 1846 mice applicable to 7833 OMIM and 4259 Orphanet Rare Disease Ontology (ORDO) terms (Fig.4). However, we could not define the 1846 mice as disease models because the mice just related to human phenotypes associated with diseases.





Figure 4. Results of ontology term mapping to the RIKEN model mice.

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

