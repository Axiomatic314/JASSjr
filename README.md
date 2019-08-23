# README #
JASSjr, the minimalistic BM25 search engine for indexing and searching the TREC WSJ collection.

Copyright (c) 2019 Andrew Trotman and Kat Lilly

Released under the 2-clause BSD licence.

Please fork our repo.  Please report any bugs.

## Why? ##
JASSjr is the little-brother to all other search engines, especially [JASSv2](https://github.com/andrewtrotman/JASSv2) and [ATIRE](http://atire.org).  The purpose of this code base is to demonstrate how easy it is to write a search engine that will perform BM25 on a TREC collection.

This particular code was originally written as a model answer to the University of Otago COSC431 Information Retrieval assignment requiring the students to write a search engine that can index the TREC WSJ collection, search in less than a second, and can rank.

As an example ranking function this code implements the ATIRE version of BM25 with k1= 0.9 and b=0.4

## Gotchas ##
* The indexer assumes that the `<DOC>` tag and the `<DOCID>` tags each have white space on each side of the `<` and `>`.  As this is the case in this collection, this isn't a problem.  It might not be the case in your data - so beware.

*  If the first word in a query is a number it is assumed to be a TREC query number

# Usage #
To build simply use

	make

To index use

	JASSjr_index <filename>
	
where `<filename>` is the name of the TREC encoded file.  The example file test_documents.xml shows the required file format.  Documents can be split over multiple lines, but whitespace is needed around `<DOC>` and `<DOCNO>` tags.

To search use

	JASSjr_search

queries a sequences of words.  If the first token is a number it is assumed to the a TREC query number and is used in the output (and not searched for).

JASSjr will produce (on stdout) a [trec_eval](https://github.com/usnistgov/trec_eval) compatible results list.

# Evaluation #
* Indexing the TREC WSJ collection of 173,252 documents takes less than 1 minute on my Mac (3.2 GHz Intel Core i5).

* Searching and generating a [trec_eval](https://github.com/usnistgov/trec_eval) compatible output for TREC queries 51-100 takes less than 3 second on my Mac.

* [trec_eval](https://github.com/usnistgov/trec_eval) reports:

---
	runid                 	all	JASSjr
	num_q                 	all	50
	num_ret               	all	1297901
	num_rel               	all	6228
	num_rel_ret           	all	5453
	map                   	all	0.2064
	gm_map                	all	0.0981
	Rprec                 	all	0.2400
	bpref                 	all	0.3043
	recip_rank            	all	0.5730
	iprec_at_recall_0.00  	all	0.6185
	iprec_at_recall_0.10  	all	0.4070
	iprec_at_recall_0.20  	all	0.3235
	iprec_at_recall_0.30  	all	0.2796
	iprec_at_recall_0.40  	all	0.2255
	iprec_at_recall_0.50  	all	0.1909
	iprec_at_recall_0.60  	all	0.1631
	iprec_at_recall_0.70  	all	0.1210
	iprec_at_recall_0.80  	all	0.0860
	iprec_at_recall_0.90  	all	0.0562
	iprec_at_recall_1.00  	all	0.0096
	P_5                   	all	0.3920
	P_10                  	all	0.3700
	P_15                  	all	0.3533
	P_20                  	all	0.3320
	P_30                  	all	0.3120
	P_100                 	all	0.2350
	P_200                 	all	0.1816
	P_500                 	all	0.1125
	P_1000                	all	0.0703
---

So JASSjr is not as fast as JASSv2, and not quite as good at ranking as JASSv2, but that isn't the point.  JASSjr is a minimalistic code base demonstrating how to write a search engine from scratch.  It performs competatively.

Copyright (c) 2019 Andrew Trotman and Kat Lilly
