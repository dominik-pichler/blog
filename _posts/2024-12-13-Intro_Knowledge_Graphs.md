
# Architecture & Graph Representation: 

## Introduction: Steering away from RDBS?
*Why should we even have a different representation like RDF or PG when we already have RDBS?*

While relational databases remain indispensable for many traditional applications, RDF and property graphs provide specialized solutions for modern challenges involving complex relationships, dynamic schemas, and semantic reasoning. The choice between these models depends on the specific requirements of your application—whether it's structured tabular data (RDB), semantic richness (RDF), or dynamic graph traversal (property graphs).

Which can be boiled down to the following advantages of RDF/PG over RDBS: 
- **Flexibility in Schema:** This flexibility is particularly useful when dealing with unstructured or semi-structured data or when the data model evolves frequently.
- **Ability to handle complex relationships**
- **Advanced Querying Capabliities** trough powerfull QLs like `SPARQL ` `Cypher`or `Gremlin `, ...
- **Easier integration of heterogeneous data sources**
- **Scaleability and Performance**: Graph databases (including RDF stores) are designed to handle large volumes of interconnected data efficiently. They avoid costly join operations required in RDBs by directly storing relationships as part of the data model. This makes them more performant for relationship-heavy queries


## Two mainstream approaches for Graph Modelling, Storing and Quering: 

**Property Graphs (PG)**
- e.g., Neo4J, JanusGraph, OrientDB
- Programmer-friendly
- Fast
- Edge’s attributes

**Resource Description Framework (RDF)**
- e.g., GraphDB, StarDog, Virtuoso
- Globally unique ID
- Interoperability-at-scale
- (shared) Schema-based

 
## (L)PG vs  RDF
There are certain advantages of the property graph over the RDF graph.
- First, the RDF triples are easy statements to produce but when the query takes place it may give a headache. 
- Secondly, since relationships in the property graphs can have properties, this may simplify the modeling process. 
- Thirdly, relationships that are repeated are counted as unique, e.g. a person like another person only one in the RDF representation
- As far as I understand (L)PG does stop the Ontology on the directly present relationships and hence cares not about broader relationsships like
   - Subclass
   - Type
   - Parent Class implications
   - ....
 
  

Why do we use the RDF triples? Because they are the so easy way to transfer and save relationships and there are already a certain amount of the RDF data sources.
 In addition, the property graphs may be a burden on the applications. 


Rambles: 
- RDF has troubles depiciting multiple identical relationsships between the same nodes
- RDF has, generally speaking Higher Ontology-Building Complexity and scale
- Most Graph Databases are based on LPG where there is no standard query language while RDF provides `SparQL`, `RDF Schema`, `OWL`, `SHACL`, `ShEX` 


#Building based on RDF: 
Every RDF based KG Graph needs a ontology. 
 
# What are ontologies? 
According to *Studer(98)*, an ontology is a "Formal, explicit specification of a shared conceptualization".

It's etymiological origin can be found (as so many things), back in old greece: 

*Ontology* = *ontos*(being) + *logos* (lit. word, discourse, or reason)
- Philosophy: Systematic explanation of Existence
   - Aristotle (400BC) attempts to establish universal categories for
classifying everything that exists

As KGs live in a world that rests on computers, designing machine-readable KGs is critical. Hence,  typically Ontologies for KGs are based on Formal Logic: 

## (Descriptive) Logic and Ontologies
Formal logics are used to form a basis for (advanced) knowledge representation. 
Thereby a formal, logic-based language provides: 
- A Syntax (Defining which Language Expressions are correct)
- A Semantic (Defining the meaning of expressions) - > TODO: Summary of Semantics of Meanings and what different concepts are linked to meaning. (This will be much! fun). For now, semantics always lives in a domain $\Delta^I$ where objects and their meaning will be mapped to this domain via an interpretation function $(\Gamma_I)$




- A Calculus (which determines how meaninigs of expressions can be determined)

For building/enriching ontolgy based knowledge representations with descriptive logics, the following elements can be used: 
$$
 1. DL ontologies are based on three kinds of building blocks:
    I.   *concepts* represent sets of individuals
    II.  *roles* represent binary relations between the individuals
    III. *individual names* represent single individuals in the domain

Unlike a database, a DL ontology does not fully describe a particular situation or
“state of the world”; rather it consists of a set of statements, called axioms, which typically capture only partial knowledge about the described situation

Although there is no principal logical difference between different types of axioms, they are often separated into three groups: assertional (ABox) axioms, terminological (TBox) axioms and
relational (RBox) axioms.


1. Asserting Facts with ABox Axioms: Knowledge about Individuals / Entities
2. Expressiong Terminal Knowledge with TBox Axioms: Knowledge about concepts of a domain.
   
    2.1. Boolean Concept Constructors

    2.2 Role Restrictions

    2.3. Nominals
3. Characterising Roles with RBox Axioms


Next, we summarise the features introduced in the previous sections to obtain a comprehensive definition of DL syntax. Doing so yields the DL called **SROIQ**, one of the most expressive DLs considered today, which is closely related to the ontology language **OWL 2 DL**.



## What can be inside an Ontology?
-  Concepts:
    -  Denote the main concepts of the domain
    - E.g.: Carnivore, Animal, Pump, Engine
-  Concept hierarchy
    - denotes specialization/generalizations
    - E.g.: Carnivore is a kind of Animal
- Relations between classes
   - E.g.: Carnivore eats Animal
- Restrictions on relations (type, cardinality) 
  -  E.g.: any Animal has at least one BodyPart
- Instances:
  - Denote concrete entities in the domain
  - E.g.: Tom, Jerry

## Examples of (Lightweight Ontologies): 
- Controlled Vocabulary: finite list of terms (e.g., a catalogue)
- Glossary:finite list of terms + informal definition in natural language
- Thesauri:
controlled vocabulary + concepts are connected with relations 
   – Equivalency (synonyms)
   – Hierarchies (subclasses, superclasses)
   – Homographs (Homonyms)
   – Associations (similar concepts) 

From there different Heavyweight Ontologies can be built by introducting extensions like: 
- Formal IS-A
- Frames
- Value Restrictions
- General logic constraints
- Disjunctiveness, Part-of,....



### Some DL practical examples: 
Symmetry
- If P(x,y) =>P(y,x)
- E.g., marriedTo, friendOf, adjacentRegion


Transitivity
- If P(x,y) and P(y,z) => P(x, z)
-  E.g., locatedIn, hasAncestor


Inverse properties
- If P(x,y) => InvP(y,x) holds
-  E.g., hasParent(John, Bob)=> hasChild(Bob, John)

  
Functional values
- can have only one (unique) value y for each instance x
- i.e. there cannot be two distinct values y1 and y2 such that the pairs (x,y1)
and (x,y2) are both instances of this property
-  E.g., hasHusband

## What can i do with ontologies? 
Thanks to the formal nature of ontologies (their grounding in logic),
reasoning can be used to infer new knowledge based on already
declared information. Reasoning is performed with reasoners (inference engines).

Reasoning allows for, e.g.,:
- Consistency checking: Checking the correctness of the ontology model
(e.g., that the model described by the ontology is free of logical
contradictions)
- Class inferences: discovering relation between classes that were not
explicitly declared.
-  Instance inferences: discovering class membership of instances.



## Building an Ontology with RDF: 

Basic RDF building block
- Subject: a resource, which may be identified with a URI
- Predicate: a URI-identified specification of the relationship between
subject and object
- Object: a resource or literal to which the subject is related

### URI: What and why?
In the semantic web, there a two basic principles regarding identifiers: 
1. Everything has an identifier
2. One Name for one resource


URI: Uniform Resource typically constists of two elements: 
- URN (RFC 2141): Uniform Resource Name
  - persistent identifier within a particular namespace
  - Refers to a resource without implying location or how to access it
  - e.g., urn:isbn:0-486-27557-4 refers to a specific edition of Shakespeare’s Romeo and Juliet
- URL (RFC 1738):
   - Uniform Resource Locator
   - specifies (primary) access mechanism
   -  may change during the lifetime of a resource


This eventually yields: $URI = URN+URL$

### RDF(S) Vocabluary: 

RDF and RDFS (its extenision), are equippted with the following 


#### **RDF Classes**
- **rdf:XMLLiteral**  
  The class of XML literal values.
- **rdf:Property**  
  The class of properties.
- **rdf:Statement**  
  The class of RDF statements.
- **rdf:Alt, rdf:Bag, rdf:Seq**  
  Containers of alternatives, unordered containers, and ordered containers (*rdfs:Container* is a super-class of the three).
- **rdf:List**  
  The class of RDF Lists.
- **rdf:nil**  
  An instance of *rdf:List* representing the empty list.

#### **RDFS Classes**
- **rdfs:Resource**  
  The class resource, everything.
- **rdfs:Literal**  
  The class of literal values, e.g., strings and integers.
- **rdfs:Class**  
  The class of classes.
- **rdfs:Datatype**  
  The class of RDF datatypes.
- **rdfs:Container**  
  The class of RDF containers.
- **rdfs:ContainerMembershipProperty**  
  The class of container membership properties (*rdf:_1*, *rdf:_2*, ...), all of which are sub-properties of *rdfs:member*.

---

#### **RDF Properties**
- **rdf:type**  
  An instance of *rdf:Property* used to state that a resource is an instance of a class.
- **rdf:first**  
  The first item in the subject RDF list.
- **rdf:rest**  
  The rest of the subject RDF list after *rdf:first*.
- **rdf:value**  
  Idiomatic property used for structured values.
- **rdf:subject**  
  The subject of the RDF statement.
- **rdf:predicate**  
  The predicate of the RDF statement.
- **rdf:object**  
  The object of the RDF statement.

> Note: *rdf:Statement*, *rdf:subject*, *rdf:predicate*, and *rdf:object* are used for reification.

---

#### **RDFS Properties**
- **rdfs:subClassOf**  
  The subject is a subclass of a class.
- **rdfs:subPropertyOf**  
  The subject is a subproperty of a property.
- **rdfs:domain**  
  A domain of the subject property.
- **rdfs:range**  
  A range of the subject property.
- **rdfs:label**  
  A human-readable name for the subject.
- **rdfs:comment**  
  A description of the subject resource.
- **rdfs:member**  
  A member of the subject resource.
- **rdfs:seeAlso**  
  Further information about the subject resource.
- **rdfs:isDefinedBy**  
  The definition of the subject resource.


### Notation Types:
- Graph notation
- RDF/XML (historically first serialization format)
-  N3/Turtle -> Many URIs share the same basis → use prefixes for namespace declarations
-  N-Triples
-  JSON-LD


For the rest of the post, I'll stick to N3/Turtle.


### N3/Turtle:
Example of N3/Turtle: 
```
exstaff:111 exterms:address exaddressid:111 .
exaddressid:111 exterms:street "Teststraße 11" .
exaddressid:111 exterms:city "Vienna" .
exaddressid:111 exterms:state "Vienna" .
exaddressid:111 exterms:postalCode "1140" . 
```

#### Edge Cases and special Graph properties: 
- RDF Blank Nodes
- Reification: Making Statements about statements
  - Alternatives:
    - Standardf reification
    - Singleton
    - Named Graphs -> Problem: Requires efficient graph indexing which is not always supported
    - RDF* `:Dominik :claims <<:Stefan :looks :happy>> `
 
 - Container   (Open Lists) 
 - Collections (Closed Lists)


## RDFs extension: OWL
Short for *Web Ontology Language*


W3C Recommendation (since 2024) for the representation of ontologies
- Fully-fledged knowledge representation language for the Web
- Provides a wider range of ontological constructs and avoids some of the potential confusion in RDFS
- Formal foundations: Description Logics (DL)
   - well-defined semantics
   - Well-understood properties (e.g., computational complexity)
   - allows to verify consistency of defined knowledge
   - inferencing allows to make implicit knowledge explicit
   - many tools available
- OWL ontologies can be exchanged as RDF documents
 
OWL extends RDF Schema to a fully-fledged knowledge representation language for the Web, icnluding Logical expressions, Local properties, Required/optional properties, Required values, Enumerated classes. Symmetry, inverse and many more ... 

Hence, this allows for a way richer approach to ontology building. 


--- 
**Great Tools**
- Protege for Ontology Building
- Caveat: Definition of infinite recursions and cycles
