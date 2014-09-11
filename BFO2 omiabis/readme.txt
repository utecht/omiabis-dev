1. List all terms in OMIABIS

2. Retrieve OBI and IAO terms used by OMIABIS from OBI using Ontodog
	- Ontodog input file: Ontodog_input_file.xlsx
	- URI of OBI subset owl: http://purl.obolibrary.org/obo/omiabis/import_OBI_subset.owl
	- Ontodog output file: import_OBI_subset.owl
Edits made in the import_OBI_subset.owl
	a. Removed all BFO terms defined in OBI since it uses BFO pre-Graz. It will remove conflict. The BFO terms are defined in the imported BFO 2 classes-only and manually imported relations if need 
	b. Removed OBI deprecated term OBI_0000300 obsolete_is_realized_by, it will be replaced by BFO_0000054
	c. Replaced OBI:disease by OGMS:disease
	
Notes: 
- OBI using pre-Graz BFO version (not released BFO2) 	
- OBI import full version of IAO based on pre-Graz BFO which may be different from last IAO release and IAO development version based on BFO 1.1. All changes OBI developers made have been incorperated in IAO development version based on BFO 1.1. 
- need to update this subset when IAO and OBI have BFO 2.0 class-only based version
- Since OBI contains full version of IAO, it allows us to retrieve all IAO terms needed by OMIABIS to simplify following integration
- OBI import terms from other OBO Foundry ontologies. CARO (1), CHEBI (5), CL (3), GAZ (1), NCBITaxon (5), OGMS (5), PATO (4), REO (2), RO (9) terms used in OMIABIS were retrieved in OBI subset. They will not be imported again using OntoFox to simlify ontology integration
- OBI has term disease. However, OMIABIS decided to use OGMS:disease. Need to replace OBI:disease by OGMS one
	
3. Import OBO terms used by OMIABIS using OntoFox
	- OntoFox input file: OntoFox_input_file.txt
	- URI of OBO import owl: http://purl.obolibrary.org/obo/omiabis/import_OBO.owl
	- OntoFox output file: import_OBO.owl

Summary of imported terms:
	a. GO (1) - MIREOT
	b. OGMS (5) - MIREOT
	c. OMRSE (4) - MIREOT (OMRSE:collection of organisms replaced by PCO:collection of organisms)
	d. PCO (1) - MIREOT
	e. PATO (6) - MIREOT	
	f. RO (10) - import all axioms
	g. BFO 2.0 relations (8) - import all axioms

Notes:
Need to clean up definition (including axioms) of BFO classes in the OntoFox output file to simplify the file, BFO classes will be only defined in the BFO 2 classes only OWL file


4. Some terms imported manually since they are not available in the triple store and cannot be retrieved using OntoFox tool
	URI of manually imported terms owl: http://purl.obolibrary.org/obo/omiabis/externalByhand.owl
	manually imported owl file: externalByhand.owl
	
Summary of manually imported terms:
	a. GEO (6) - including 4 OMRSE deprecated terms
	b. PNO (5) - IAO domain IDs >= 0020000
	c. APOLLO_SV (3) - All Axioms


Notes: 
Following terms were deprecated from OMRSE, 
	http://purl.obolibrary.org/obo/OMRSE_00000028 #geopolitical organization
	http://purl.obolibrary.org/obo/OMRSE_00000029 #sovereign state
	http://purl.obolibrary.org/obo/OMRSE_00000030 #subnational entity
	http://purl.obolibrary.org/obo/OMRSE_00000032 #geopolitical dependency
terms were added in GEO
	http://purl.obolibrary.org/obo/GEO_000000396 #sovereign state
	http://purl.obolibrary.org/obo/GEO_000000004 #subnational entity
	http://purl.obolibrary.org/obo/GEO_000000006 #geopolitical dependency	
So, these OMRSE terms are replaced by GEO terms in OMIABIS
	
5. Clean up omiabis.owl which contains OMIABIS specific terms only
	import following OWL files:
	- http://purl.obolibrary.org/obo/bfo/2014-05-03/classes-only.owl
	- http://purl.obolibrary.org/obo/omiabis/import_OBI_subset.owl
	- http://purl.obolibrary.org/obo/omiabis/import_OBO.owl
	- http://purl.obolibrary.org/obo/omiabis/externalByHand.owl
	
6. Using 'mapping.txt' mapping file to update all terms using BFO 2.0 and RO 2.0 terms (by running Converter implemented using OWL-API)

After these steps, Hermit was used to check consistency. It looks good.

Issue:
No mapped BFO 1.1: ConnectedTemporalRegion term in BFO 2.0. 
Please see BFO1.1 to BFO2.0 mapping file (has been reviewed by Alan)
https://docs.google.com/spreadsheets/d/1UhdsxU0o6T9XNuOjNy24tAqWS0nnHQ-WHb77_VQGJo0/edit#gid=1715696033