[gimmick: math]()

## ER

- Entity: 
    - person/place/thing
    - **rectangle**

- Entity set:
    - a group consisting of similar entities

- Attributes:
    - characteristic describing an entity set 
    - **oval**
    - domain : allowed value

- Multivalued attributes:
    - double oval

- derived attribute:
    - dashed oval

- relation
    - **diamond**

- weak entity
    - no primary key
    - dependent on a strong entity
    - **double diamond**

--||--  mandatory one
--||-<E mandatory many

-o-|--  optional one
-o-|-<E optional many

- - - -

## Keys

Attribute is **prime** if is part of any key.

1. \\(X\\) is a key if it functionally determines all attributes in \\(R\\)
2. \\(X\\) is minimal with respect to condition 1.

### Table method

Make a table: Left, Middle, Right

L : Attributes that only appear on LHS
M : Attributes that appear on either side
R : Attributes that only appear on RHS

Attributes that are only on L **must be** part of any key.
Attributes that are only on R **must not** be part of any key. 

- - - -

## Covers:

- 2 sets of FDs \\(F,G\\) are equivalent if \\(F\\) covers \\(G\\) and \\(G\\) covers \\(F\\).
- That is:
  - \\(F\\) is a subset of \\(G^{+}\\) 
  - \\(G\\) is a subset of \\(F^{+}\\)

### Example

- \\( F = \\{ A \rightarrow B, B \rightarrow C, C \rightarrow A \\} \\)
- \\( G = \\{ C \rightarrow B, B \rightarrow A, A \rightarrow C \\} \\)


1. Take LHSes of \\(F\\), do their closures with respect to \\(G\\).
  - \\(A^{+} = ACB\\).
    - This contains the RHS of \\(F \\{ A->B \\}\\), so we know it'll be in \\(G^{+}\\).
  - \\(B^{+} = BAC\\)
    - This contains the RHS of \\(F \\{ B->C \\}\\), so we know it'll be in \\(G^{+}\\).
  - \\(C^{+} = CBA\\)
    - This contains the RHS of \\(F \\{ C->A \\}\\), so we know it'll be in \\(G^{+}\\).
  - 
  - So we know \\(F\\) is a subset of \\(G^{+}\\), or that \\(G\\) **covers** \\(F\\).
2. Take LHSes of \\(G\\), do their closures with respect to \\(F\\).
  - \\(C^{+} = CAB \hspace{5mm} G \\{C \rightarrow B\\} \\)
  - \\(B^{+} = BAC \hspace{5mm} G \\{B \rightarrow A\\} \\)
  - \\(A^{+} = ACB \hspace{5mm} G \\{A \rightarrow C\\} \\)
  - 
  - So we know \\(G\\) is a subset of \\(F^{+}\\), or that \\(F\\) **covers** \\(G\\).

Therefore we have proven that \\(F\\) is **equivalent** to \\(G\\). 

## Normal form shortcuts:

|Characteristic|Result|
|--------------|------|
|All attributes are prime| (at least) 3NF|
|Singleton keys| (at least) 2NF|

1NF  : All attributes are atomic.
2NF  : If RHS is a non-prime, then LHS is not a proper subset of any key.
3NF  : If RHS is a non-prime, then LHS is a superkey.
BCNF : LHS is a superkey.

## Second Normal Form. 

- No partial key dependencies. 

### Checking: 

- \\( R(A,B,C,D,E) \\)
- \\( F = \\{ ABD \rightarrow C, BC \rightarrow D, CD \rightarrow E \\} \\)

1. Find keys
  - Try \\( AB^{+} = AB \\)      ❌
  - Try \\( ABC^{+} = ABCDE \\)  ✅
  - Try \\( ABD^{+} = ABDCE \\)  ✅


- Keys are \\(ABC,ABD\\).
- So the prime attributes are \\(ABCD\\), and the only non-prime is \\(E\\). 
- If the LHS is a proper subset of a key, and RHS is non-prime, 2NF is violated. 
- Take closures of proper subsets of keys:

- \\(ABC\\) : 
  - \\(AB^{+} : AB\\)   ✅ ( no non-primes )
  - \\(AC^{+} : AC\\)   ✅ ( no non-primes )
  - \\(BC^{+} : BCDE\\) ❌ ( E is nonprime )

So this violates 2NF. 

## Third Normal Form

For each FD \\(X \rightarrow A\\):

- If \\(A\\) is be non-prime, \\(X\\) must be a superkey (or a key) 

### Example

- \\(R(ABC)\\)
- \\(F = \\{ A \rightarrow B, B \rightarrow C \\}\\)
- 
- \\(A\\) is prime, \\(BC\\) are non-prime.
- In \\(B \rightarrow C\\), \\(C\\) is non-prime, and \\(B\\) is not a superkey, so this **violates** 3NF.

### Bernsteins Synthesis

- **Guarantees** : dependency preserving
- **Does Not Guarantee** : lossless

- Summary:
  1. Make sure FDs are a minimal cover
  2. Take each FD and make it its own subschema
  3. try to combine subschemas

Ex:

- \\(R(ABCDE)\\)
- \\(F = \\\{ A \rightarrow B, A \rightarrow C, DE \rightarrow C, DE \rightarrow B, C \rightarrow D \\\}\\)

<ol> 
<li> Find keys. <table style="width: 25%">
  <thead>
    <th>L</th>
    <th>M</th>
    <th>R</th>
  </thead>
  <tbody>
    <tr>
      <td> AE</td>
      <td> CD</td>
      <td> B</td>
    </tr>
  </tbody>
</table>
<ul> <li> \\(AE^{+} = AEBCD\\), so \\(AE\\) is a key.</li>
    <li> Therefore: 
      <ul><li>Prime    : \\(AE\\)</li>
        <li>Nonprime : \\(BCD\\)</li>
      </ul>
    </li>
</li>
</ul>
<li>Test for 2NF
  <ul>

  <li>\\(A\{+} = ABCD\\)</li>
  <li>\\(E\{+} = E\\)</li>
  <li>A proper subset of the key (\\(A^{+}\\)) contains non-prime attributes (\\(BCD\\)), so 2NF is violated. </li>
</ul>
</li>

<li> Make a relation subschema for each FD. 

<ul>
  <li>\\(R1(\underline{A}B)\\)</li>
  <li>\\(R2(\underline{A}C)\\)</li>
  <li>\\(R3(\underline{DE}C)\\)</li>
  <li>\\(R4(\underline{DE}B)\\)</li>
  <li>\\(R5(\underline{C}D)\\)</li>
</ul>
<br/>

<ul>
  <li>\\(R1,R2\\) share a LHS so we can combine them: \\(S(\underline{A}BC)\\)</li>
  <li>\\(R3,R4\\) share a LHS so we can combine them: \\(T(\underline{DE}BC)\\)</li>
  <li>All attributes in \\(R5\\) are contained in \\(T\\), so we can discard it.</li>
</ul>

</li>
</ol>

Decomposition of \\(R\\) to \\(S(\underline{A}BC),T(\underline{DE}BC)\\), but it's lossy.

To make this lossless, we can add a schema \\(U\\) with the key : \\(U(AE)\\). This only works with Bernstein's synthesis. 

## BCNF

Every LHS has to be a superkey (or a key)

### Paired attribute algorithm

- **Guarantees** : lossless
- **Does Not Guarantee** : dependency preserving

\\(R(ABCD)\\)
\\(F = \\{ A \rightarrow C, BC \rightarrow A, C \rightarrow D\\}\\)

1. Set up a variable \\(Z\\) that contains all attributes of \\(R\\).

\\(Z = ABCD\\)

2. Take \\(R - \text{ first pair in } Z \\)

\\(R - AB = CD\\)

3. Take closure of result. If that closure contains the subtracted value(s),
we have a violation and need to decompose. 

\\(CD^{+} = CD\\). So \\(AB\\) is OK.

Repeat (2,3) for next pair.

\\(R - AC = BD\\)

\\(BD^{+} = BD\\). So \\(AC\\) is OK.

Repeat (2,3) for next pair. 

\\(R - AD = BC^{+} = ABCD\\). So we have a violation, and need to decompose. 

-----

Decompose(\\(ABCD\\)

(i) Make a separate variable, e.g. \\(Y\\), containing the attributes of \\(Z\\).

\\(BC^{+} = ABCD = Y\\)

(ii) Offending LHS attributes are \\(A,D\\). Choose one to remove; let's go with \\(D\\).

\\(Y = ABC\\). 

(iii) Do \\(Y - pairs\\)

\\(Y - AB = C\\)
\\(C^{+} = C\\), so \\(AB\\) is OK.

\\(Y - AC = B\\)
\\(B^{+} = B\\), so \\(AC\\) is OK.

\\(Y - BC = A\\)
\\(A^{+} = ACD\\). \\(ACD\\) contains \\(C\\), so we get rid of the \\(B\\).

We're left with \\(AC\\), which was the last thing we included before the decomposition, so we need to remove \\(C\\) from \\(Z\\).

\\(R_1(AC)\\)

-----

Continuing:

1. \\(Z = ABD\\)

2. \\(R - \\text{ pairs in } Z\\)

\\(R - AB = D\\)
\\(D^{+} = D\\), so \\(AB\\) is OK.

\\(R - AD = B\\)
\\(B^{+} = B\\), so \\(AD\\) is OK.

\\(R - BD = A\\)
\\(A^{+} = ACD\\). \\(ACD\\) contains \\(D\\), so we need to call decompose again.

----

Decompose(\\(ABD\\))

(i) \\(Y = ABD\\)

(ii) Offending LHS attributes are \\(B,D\\). Since \\(R-BD = A\\) and \\(A+\\) contains \\(D\\), we'll remove the \\(B\\).

\\(Y = AD\\).

Since this is a pair, we can return it, and give it a new relation.

\\(R_1(AC), R_2(AD)\\)

- - - -

Continuing: 

\\(Z = AB\\), which is already a pair, so we can use \\(Z\\) as \\(R3\\).

Therefore our BCNF decomposition of \\(R\\):

\\(R_1(AC), R_2(AD), R_3(AB)\\).

n.b. It might not necessarily leave just pairs, but as long as the tests pass, don't worry about it.

## Decomposition - lossless

Lossless : do a join of all subschemas and we get back the same thing. 

### Checking for lossless decomposition

\\(R(A,B,C,D,E) \\)
\\(F = \\{ AB \rightarrow C, C \rightarrow E, B \rightarrow D, E \rightarrow A \\} \\)
\\(R1(BCD),R2(ACE) \\)

|Subschema| A | B | C | D | E |
|---------|---|---|---|---|---|
|\\(R_1\\)|   |   |   |   |   |
|\\(R_2\\)|   |   |   |   |   |

For each instance where R1,R2 has an attribute, put a lowercase 'a'.

|Subschema| A | B | C | D | E |
|---------|---|---|---|---|---|
|\\(R_1\\)|   |`a`|`a`|`a`|   |
|\\(R_2\\)|`a`|   |`a`|   |`a`|

Goal is a full row of `a`s.

#### Rules for adding DVs:

1. 2 or more rows with distinguished variable for _LHS_ of FD
2. 1 or more rows with distinguished variable for _RHS_ of FD
3. 1 or more rows with non-distinguished varible for _RHS_ of FD



- Taking \\(AB \rightarrow C\\):
  - Rule 1: ❌
  - Rule 2: ✅
  - Rule 3: ❌

- Taking \\(C \rightarrow E\\):
  - Rule 1: ✅
  - Rule 2: ✅
  - Rule 3: ✅

So we can add a DV to \\(R_1(e)\\):

|Subschema| A | B | C | D | E |
|---------|---|---|---|---|---|
|\\(R_1\\)|   | a | a | a | a |
|\\(R_2\\)| a |   | a |   | a |

- Taking \\(B \rightarrow D\\):
  - Rule 1: ❌
  - Rule 2: ✅
  - Rule 3: ✅

- Taking \\(E \rightarrow A\\):
  - Rule 1: ✅
  - Rule 2: ✅
  - Rule 3: ✅

So we can add a DV to \\(R_1(a)\\):

|Subschema| A | B | C | D | E |
|---------|---|---|---|---|---|
|\\(R_1\\)| a | a | a | a | a |
|\\(R_2\\)| a |   | a |   | a |

We have a full row of DVs, so we can now say this is a **lossless decomposition**. N.B you can loop over FDs multiple times

## Decomposition - dependency preserving

Using the same example from above. 

\\( R(A,B,C,D,E) \\)
\\( F = \\{ AB \rightarrow C, C \rightarrow E, B \rightarrow D, E \rightarrow A\\} \\)
\\( R1(BCD),R2(ACE) \\)

1. Take the LHS of the first FD and intersect it with \\(R_1\\)

\\(Z = AB \cap R_1 = AB \cap BCD = B\\)

2. Take closure of the result.

\\(B^{+} = BD\\)

3. Take the result of (2) and intersect it with \\(R_1\\).

\\(BD \cap R_1 = BD \cap BCD = BD\\)

\\(Z = ABD. Repeat with \\(R_2\\).

1. Take \\(Z and intersect it with \\(R_2\\)

\\(Z \cap R_2 = A \\)

2. Take closure of result

\\(A^{+} = A. No change, so we repeat the process starting with \\(R_1\\).

1. Intersect \\(Z with \\(R_1\\)

\\(Z = ABD\\)
\\(ABD \cap R_1 = BD\\)

2. Take closure of the result:

\\(BD^{+} = BD\\). 
No change, so repeat the process with \\(R_2\\).

1. Intersect \\(Z with \\(R_2\\). 

\\(Z = ABD\\)
\\(ABD \cap R_2 = A\\)
Still no change, so having looped over once we can say that dependencies are **not** preserved
by this decomposition. 

This can be repeated for each FD to check if it is preserved. 

### Shortcut

If the LHS and RHS are preserved in one of the schemas, the FD is preserved. So in the above example we can see that \\(B \rightarrow D\\) is preserved in \\(R_1\\), and \\(C \rightarrow E\\), and \\(E \rightarrow A\\) are preserved in \\(R_2\\). 

## Minimal covers

- Summary:
    1. Singleton RHS
    2. No extraneoud LHS attributes
    3. No redundant FDs

n.b. Minimal covers are not unique. 
**Important to do steps in order**

\\(R(ABCDE)\\)
\\(F = \\{ A \rightarrow D, BC \rightarrow AD, C \rightarrow B, E \rightarrow A, E \rightarrow D \\}\\)

1. Make sure all FDs have singleton RHS.

\\(F = \\{ A \rightarrow D, BC \rightarrow A, BC \rightarrow D, C \rightarrow B, E \rightarrow A, E \rightarrow D \\}\\)

2. Using FDs that have 2+ members on the LHS, see if any are extraneous. (one at a time) 

Taking \\(BC \rightarrow A\\).

3. Take closure of members of LHS.

\\(B^{+} = B\\)
\\(C^{+} = CBAD\\)

4. Since the closure of \\(C\\) contains \\(B\\) (and \\(A)\\) we can remove \\(B\\) from the LHS.

\\(F = \\{ A \rightarrow D, C \rightarrow A, BC \rightarrow D, C \rightarrow B, E \rightarrow A, E \rightarrow D \\}\\)

Move on to \\(BC \rightarrow D\\), and repeating (3):

\\(B^{+} = B\\)
\\(C^{+} = BCAD\\)

Since \\(C+\\) contains \\(B\\), we can remove it from the LHS.

\\(F = \\{ A \rightarrow D, C \rightarrow A, C \rightarrow D, C \rightarrow B, E \rightarrow A, E \rightarrow D \\}\\)

5. Check for redundant FDs by doing the closure with and without that dependency.

with:    \\(A^{+} = AD\\)
without: \\(A^{+} = A\\), so we need to keep \\(A \rightarrow D\\).

with:    \\(C^{+} = CADB\\)
without: \\(C^{+} = CDB\\), so we need to keep \\(C \rightarrow A\\).

with:    \\(C^{+} = CADB\\)
without: \\(C^{+} = CADB\\), so we \\(C \rightarrow D\\) is redundant.

with:    \\(C^{+} = CADB\\)
without: \\(C^{+} = CAD\\), so we need to keep \\(C \rightarrow B\\).

with:    \\(E^{+} = EAD\\)
without: \\(E^{+} = E\\), so we need to keep \\(E \rightarrow A\\).

with:    \\(E^{+} = EAD\\)
without: \\(E^{+} = EAD\\), so we \\(E \rightarrow D\\) is redundant.

Our set of FDs becomes:

\\(F = \\{ A \rightarrow D, C \rightarrow A, C \rightarrow B, E \rightarrow A \\} \\)

### Shortcut

If a variable only appears once on RHS, we need to keep that one. 
So using the above example, we need to keep \\(C->B\\) right off the bat. 

## Joins

Given: 

Faculty table: 

|SSN|Rank|
|---|----|
|111|Asst|
|333|Full|
|555|Assoc|

Student table:

|SSN|GPA|
|---|----|
|333|3.9|
|444|3.2|
|777|3.6|

### Faculty LEFT OUTER JOIN Student

**LEFT** table is preserved, right is padded where values don't match.

|F.SSN|Rank|S.SSN|GPA|
|-----|----|-----|---|
| 111 |Asst|     |   |
| 333 |Full| 333 |3.9|
| 555 |Assc|     |   |

### Faculty RIGHT OUTER JOIN Student

**RIGHT** table is preserved, left is padded where values don't match.

|F.SSN|Rank|S.SSN|GPA|
|-----|----|-----|---|
|     |    | 333 |3.9|
|333  |Full| 444 |3.2|
|     |    | 777 |3.6|

### Faculty FULL OUTER JOIN Student

**BOTH** tables are preserved, and both are padded where values don't match.

|F.SSN|Rank|S.SSN|GPA|
|-----|----|-----|---|
| 111 |Asst|     |   |
| 333 |Full| 333 |3.9|
| 555 |Assc|     |   |
|     |    |     |   |
|     |    | 444 |3.2|
|     |    | 777 |3.6|







