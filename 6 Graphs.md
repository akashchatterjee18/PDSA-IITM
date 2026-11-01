# Graphs

## Visualising relations as graph.

- **Teachers and courses.**
  - T: set of teachers in a college.
  - C: set of courses being offered.
  - A ⊆ T × C: A describes the allocation of teachers to courses.

  → A = {(t,c) | (t,c) ∈ T × C}

<img width="283" height="238" alt="image" src="https://github.com/user-attachments/assets/c499ca4d-8e9d-4fce-b039-770db0284615" />


- **Friendships.**
  - P: set of students.
  - F ⊆ P × P : F describes which pairs of students are friends.

  → F = {(p,q) | {p,q} ∈ P, p ≠ q}

  → (p,q) ∈ F iff (q,p) ∈ F

<img width="283" height="238" alt="image" src="https://github.com/user-attachments/assets/4bad5e0c-833b-4785-bf69-0a5242241910" />

---

## Directed Graph

(v,v') ∈ E doesn't imply (v',v) ∈ E

Eg:- The teacher-course graph is directed graph.

## Undirected Graph.

(v,v') ∈ E iff (v',v) ∈ E

Effectively (v,v'), (v',v) are the same edge.

Eg:- The Friendship graph is undirected graph.

## Path

A path is a sequence of vertices v₁, v₂, ..., vₖ connected by edges.

for 1 ≤ i < k, (vᵢ, vᵢ₊₁) ∈ E

→ Normally a path doesn't visit a vertex twice.

→ A sequence that re-visits a vertex is usually called a walk.

Eg:- Kumar – Feroze – Colin – Aziz – Priya – Feroze – Sheila

---

# Reachability.

Reachability is the property of graph that tells us whether we can travel from one vertex (node) to another by following the edges.

→ A vertex v is reachable from vertex u, if there exists a path from u to v.

→ Airline routes.

**How can I fly from Madurai (v₄) to Delhi (v₀)**

### Typical Questions

- Is v reachable from u?
- Shortest path from u to v?
- What are the vertices reachable from u?
- Is the graph connected?

---

# Map colouring.

→ Assign each state a colour.

→ States that share a border should be coloured differently

→ How many colours do we need??

- Create a graph where each state is a vertex and connect states that share a border.
- Assign colours to nodes, so that endpoints of an edge have different colours.
- Only need the underlying graph.
