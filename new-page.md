---
title: Untitled Page
description: 
published: false
date: 2025-06-27T05:41:23.524Z
tags: 
editor: markdown
dateCreated: 2025-06-27T05:41:23.524Z
---

# Header
Your content here

<div id="box" style="width:400px; height:400px;"></div>
<script src="https://cdn.jsdelivr.net/npm/jsxgraph/distrib/jsxgraph.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/jsxgraph/distrib/jsxgraph.css" />
<script>
  const board = JXG.JSXGraph.initBoard('box', { boundingbox: [-5, 5, 5, -5], axis: true });
  const A = board.create('point', [0, 0], {name: 'A'});
  const B = board.create('point', [4, 0], {name: 'B'});
  const C = board.create('point', [2, 3], {name: 'C'});
  board.create('polygon', [A, B, C]);
</script>