---
title:  Neeva OA Project: Text Editor
tags:
  - Golang

---



## Text Editor Optimization



### Introduction

  In response to the needs of QwickType engineers for a large amount copying andpasting code, this project optimized the existing text editor method, improvedthe performance of CopyPaste, CutPaste operations through linked list, andsupplemented the method of `ReplaceAll` and `DeleteMatched`.



### Optimization Process

- Modified the data structure of the text editor, keeping the **dictionary** as `map[string]bool`, and changing the **document** and **pasteText** to `*ByteNode`.

- Implement various method of `*ByteNode`:

  1.`newByteNodeList`: create a new node and insert at the end;

  2.`insertLast`: insert given node at the end of the previous linked list;

  3.`replace`: check whether the value of node equals the given node, and handle two situations where new node's length is longer or shorter than the old node's length;

  4.`insert`: insert node of the index

  5.`delete`: delete node of the index

  6.`get`: get node of the index

- Overwrite the original method:`Cut`, `Copy`, `Paste`, `GerText` and `Misspelling`, and increase the method`ReplaceAll`, `DeleteMatched`.

- Run the code and test the result.



### Result Comparison

**Original Result**:

<img src="/assets/image/2020-10-11-1.jpg" width="60%" height="60%" div align=center>

**Result after optimization**:

<img src="/assets/image/2020-10-11-2.jpg" width="60%" height="60%" div align=center>

### Instructions

Running the starter code: 

`go test -bench=. editor_test1.go`



### Conclusion

  According to the test results, we can compare that the performance of `CutPaste` and `CopyPaste` operations has been greatly improved, and the overall text editing has also been greatly improved; at the same time, the efficiency of checking `Misspellings` and `GetText` has decreased. This is a kind of tradeoff. In the actual optimization process, I considered that the CutPaste and CopyPaste operations of the text account for a large proportion. In contrast, the optimization of these two operations is more important and will maximize the overall performance. At the same time, the addition of `ReplaceAll` and `DeleteMatched` methods will also make the text editor more effective.
