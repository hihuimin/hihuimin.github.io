---
layout: default
title: "document.designMode"
---

头一次听说这个属性。。默认为`off`或`inherit`，将它设为`on`可对整个文档进行编辑，与下列代码等效：

    document.body.contentEditable = true;

通常会将其应用至`iframe`，如富文本编辑器:

    iframeNode.contentDocument.designMode = 'on';
