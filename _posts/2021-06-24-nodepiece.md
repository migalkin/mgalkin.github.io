---
title: 'NodePiece - Tokenizing Knowledge Graphs'
date: 2021-06-24
permalink: /posts/2021/06/24/post/
tags:
  - tokenization
  - nodepiece
  - knowledge graph
  - research
  - graph ml
---

A new [blogpost](https://towardsdatascience.com/nodepiece-tokenizing-knowledge-graphs-6dd2b91847aa) on our recent research idea: if nodes in a graph are "words", can we design a fixed-size vocab of "sub-word" units and go beyond shallow embedding? We propose NodePiece, a compositional tokenization approach for dramatic KG vocabulary size reduction, and find that in some tasks, you don't even need trainable node embeddings! Furthermore, NodePiece is inductive by design and can encode unseen nodes using the same backbone vocabulary.