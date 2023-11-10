1. (2 points) Perform constant folding & propagation analysis using the worklist algorithm. Write each basic
block’s pre state in the fixpoint.

**main() entry pre-state:**
_1, _ret11, _t10, _t2, _t3, _t4, _t5, _t6, _t7, _t8, _t9, a, b, c, d, e: 0


**bb1 pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* b: T (unknown)
* _t6: T (unknown)
* _t7: T (unknown)
* e: T (unknown)
* _t8: T (unknown)
* _t9: T (unknown)
* _t10: 0
* _ret11: 0


**bb2 pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* b: T (unknown)
*  **_t6: 1 // has to be true in order to go into bb2**
*  _t7: T (unknown)
*  e: T (unknown)
* _t8: T (unknown)
* _t9: T (unknown)
* _t10: 0
* _ret11: 0


**bb6 pre-state:** highlighted changes
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* **b: 2**
* _t6: 1 // has to be true in order to go into bb2
* **_t7: T (unknown)**
* **e: T (unknown)**
* **_t8: 1 // has to be true in order to go into bb6**
* _t9: 0
* _t10: 0
* _ret11: 0


**bb7 pre-state:** highlighted changes
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* b: 2
* _t6: 1 // has to be true in order to go into bb2
* _t7: T (unknown)
* e: T (unknown)
* _t8: 1 // has to be true in order to go into bb6
* **_t9: T (unknown)**
* _t10: 0
* _ret11: 0


**bb5 pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* **b: T (unknown)**
* _t6: 1 // has to be true in order to go into bb2
* _t7: T (unknown)
* e: T (unknown)
* _t8: 1 // has to be true in order to go into bb6
* _t9: T (unknown)
* _t10: 0
* _ret11: 0


**bb8 pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* **b: 2**
* _t6: 1 // has to be true in order to go into bb2
* **_t7: T (unknown)**
* **e: T (unknown)**
* **_t8: 0 // has to false in order to go into bb8**
* _t9: 0
* _t10: 0
* _ret11: 0


**bb3 pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* **a: T (unknown)**
* _t5: T (unknown)
* b: T (unknown)
* _t6: T (unknown)
* _t7: T (unknown)
* e: T (unknown)
* _t8: T (unknown)
* _t9: T (unknown)
* **_t10: T (unknown)**
* _ret11: 0


**exit pre-state:**
* _t2: memory address, so T (unknown)
* c: memory address, so T (unknown)
* d: memory address, so T (unknown)
* _t3: 3
* _t4: 6
* a: T (unknown)
* _t5: T (unknown)
* b: T (unknown)
* _t6: T (unknown)
* _t7: T (unknown)
* e: T (unknown)
* _t8: T (unknown)
* _t9: T (unknown)
* _t10: T (unknown)
* **_ret11: T (unknown)**



2. (2 points) Perform constant folding & propagation optimization using the results from question 1. Draw the
CFG of the resulting program.


// replace two instructions in main() entry block


3. (2 points) Use the result of question and perform reaching definitions analysis. Write the final pre state for
each basic block.


**main() entry pre-state:**
_1, _ret11, _t10, _t2, _t3, _t4, _t5, _t6, _t7, _t8, _t9, a, b, c, d, e |-> 0 (empty set)


**bb1 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {entry.9, bb7.1}
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2}
* e      |-> {bb2.3}
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1}
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb2 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {entry.9, bb7.1}
* _t6    |-> {bb1.1} // UPDATED
* _t7    |-> {bb2.2}
* e      |-> {bb2.3}
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1}
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb6 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb2.1} // UPDATED
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2} // UPDATED
* e      |-> {bb2.3} // UPDATED
* _t8    |-> {bb2.4} // UPDATED
* _t9    |-> {bb6.1}
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb7 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb2.1}
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2}
* e      |-> {bb2.3}
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1} // UPDATED
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb5 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb7.1} // UPDATED
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2}
* e      |-> {bb2.3}
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1} // UPDATED
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb8 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb2.1} // UPDATED
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2} // UPDATED
* e      |-> {bb2.3} // UPDATED
* _t8    |-> {bb2.4} // UPDATED
* _t9    |-> {bb6.1}
* _t10   |-> 0 (empty set)
* _ret11 |-> 0 (empty set)


**bb3 pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb2.1}
* _t6    |-> {bb1.1} // UPDATED
* _t7    |-> {bb2.2}
* e      |-> {bb2.3, bb8.2} // UPDATED
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1}
* _t10   |-> {bb8.1} // UPDATED
* _ret11 |-> 0 (empty set)


**exit pre-state:**
* _t2    |-> {entry.1}
* c      |-> {entry.7}
* d      |-> {entry.3}
* _t3    |-> {entry.4}
* _t4    |-> {entry.5}
* a:     |-> {entry.6, bb5.1}
* _t5    |-> {entry.8}
* b:     |-> {bb2.1}
* _t6    |-> {bb1.1}
* _t7    |-> {bb2.2}
* e      |-> {bb2.3, bb8.2}
* _t8    |-> {bb2.4}
* _t9    |-> {bb6.1}
* _t10   |-> {bb8.1}
* _ret11 |-> {bb3.1} // UPDATED


4. (2 points) Use the result of the previous question and perform liveness analysis. Write the final post state for
each basic block.

**exit post-state:** 0 (empty set)
+ exit.1 needs _ret11 |-> {bb3.1}
+ {bb3.1}

**bb3 post-state:** {bb3.1}
+ bb3.1 needs e |-> {bb2.3, bb8.2}
+ {bb2.3, bb8.2}

**bb8 post-state:** {bb2.3, bb8.2}
+ bb8.2 needs bb8.1 |-> 0 (empty set)
+ bb8.1 needs nothing
+ {bb2.3}

**bb5 post-state:** {bb8.2, bb2.3, entry.6, bb5.1}
+ bb5.1 needs bb7.1
+ {bb8.2, bb2.3, entry.6, bb7.1}

**bb7 post-state:** {bb8.2, bb2.3, entry.6, bb7.1}
+ bb7.1 needs bb6.1
+ {bb8.2, bb2.3, entry.6, bb6.1}

**bb6 post-state:** {bb8.2, bb2.3, entry.6, bb6.1}
+ bb6.1 needs a |-> {entry.6, bb5.1}
+ {bb8.2, bb2.3, entry.6, bb5.1}

**bb2 post-state:** {bb8.2, bb2.3, entry.6, bb5.1}
+ bb2.5 needs bb2.4 |-> 0 (empty set)
+ bb2.4 needs nothing
+ bb2.3 needs bb2.2
+ bb2.2 needs e |-> {bb2.3} and b |-> {bb2.1}
+ bb2.1 needs nothing
+ {bb8.2, bb2.3, entry.6, bb5.1}

**bb1 post-state:** {bb8.2, bb2.3, entry.6, bb5.1}
+ bb1.2 needs bb1.1
+ bb1.1 needs e |-> {bb2.3} and a |-> {entry.6, bb5.1}
+ {bb8.2, bb2.3, entry.6, bb5.1}

**entry post-state:** {bb8.2, bb2.3, entry.6, bb5.1}
+ entry.10 needs nothing
+ entry.9 needs _t5 --> entry.8
+ entry.8 needs d --> entry.3
+ entry.7 needs c |-> {entry.3} and a |-> {entry.6}
+ entry.6 needs nothing
+ entry.5 needs nothing
+ entry.4 needs nothing
+ entry.3 needs c --> entry.2
+ entry.2 needs _t2 --> entry.1
+ entry.1 needs nothing
+ {bb8.2, bb2.3, bb5.1}


5. (2 points) Use the result of the previous question and perform dead store elimination. Draw the CFG of the
resulting program.


look at the post-state of each instruction.

does it contain instructions from the liveness post-state? if not, instruction isnt necessary. so we can delete

X = what lines to remove