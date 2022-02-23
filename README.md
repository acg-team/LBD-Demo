# LBD-Demo
A simple visualization for demonstrating LBD use cases

### stack of technologies
- Django as the backend
- D3.js as the frontend
- Neo4j as the graph database

## Data model

#### Data description
A simple data model here is designed based on a well-known Swanson model. It has three sets of entity types (medicine, natural product, ...) and five relationships (contains, improves, ...) which define binary relationships among different entity types. 
CSV format is chosen to be compatible to neo4j data intake procedure. The relevant command can handle up to a couple of million entities and relationships.

![alt text](https://github.com/acg-team/LBD-Demo/blob/main/graph.png?raw=true)

#### Data intake

1. Define classes and relationships in CSV format similar to what is already done in csv_intake
2. Create a free tier neo4j db at Neo4j AuraDB
3. Entity intake

```LOAD CSV WITH HEADERS FROM '{url of csv raw format for an entity file with entity type X}' AS row CREATE (v:X) SET v.name = row.x, v.description = row.description```

4. Relationship intake

```LOAD CSV WITH HEADERS FROM '{url of csv raw format for a relationship file with relation type X}' AS row MATCH (s:{Source entity type} {name: row.{source entity type}}) MERGE (t:{Target entity type} {name: row.{target entity type}}) WITH s, t MERGE (s)-[:X]->(t)```

4. Validate the intake 

```MATCH (Subject)-[Predicate]->(Object) RETURN Subject, Predicate, Object LIMIT 5```

## Frontend
- http://shorturl.at/eiDKX
