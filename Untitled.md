
## 1
Create --> Crea la relazione e i nodi se non esistono
- OpType = CREATE
- Entity = RELATIONSHIP
- UserProperties (e.g. number_interactions as score ) {
-      id
- }
- NodeType [model_name ] Recipe  | Post | Collection | Contest
- NodeProperties (
-     id
- )
- RelationshipType (e.g. 'likes', 'bookmarks') e.g. VERBO
- RelationshipProperties []

Utente ha partecipato al contest

## 2
DELETE --> Cancella solo la relazione tra nodo e relationship
Entity = RELATIONSHIP
OpType = DELETE
UserId
NodeType
NodeId
RelationshipType ('likes')

DELETE NODE --> Cancella il nodo
Entity = NODE
OpType = DELETE
NodeType
NodeId

## 3
UPDATE --> Se esiste il nodo, lo aggiorno se no lo creo. Crea un nodo senza relazioni
NodeType
NodeId
NodeProperties





# DNS
- Linkare Cloudflare ai DNS di AWS
```
ns-1802.awsdns-33.co.uk.
ns-1484.awsdns-57.org.
ns-1.awsdns-00.com.
ns-870.awsdns-44.net.
```
- Emanare certificato SSL AWS
- Aggiungere il certificato agli Ingress dell'infrastruttura
- Cambiare gli hostname negli ingress
