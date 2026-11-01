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

## Reachability.

Reachability is the property of graph that tells us whether we can travel from one vertex (node) to another by following the edges.

→ A vertex v is reachable from vertex u, if there exists a path from u to v.

→ Airline routes

<img width="271" height="267" alt="image" src="https://github.com/user-attachments/assets/ae3e0e83-1d36-4675-b6bd-d3bbdc7a57d8" />

**How can I fly from Madurai (v₉) to Delhi (v₀)**
Typical Questions
- Is v reachable from u?
- Shortest path from u to v?
- What are the vertices reachable from u?
- Is the graph connected?

---

## Map colouring.

→ Assign each state a colour.

→ States that share a border should be coloured differently

→ How many colours do we need??

- Create a graph where each state is a vertex and connect states that share a border.
- Assign colours to nodes, so that endpoints of an edge have different colours.
- Only need the underlying graph.

## Graph Colouring

We are given a graph G = (V, E) and a set of colours C and we need to assign a colour to every vertex such that no pair of adjacent vertices have the same colour.

Colouring is a fⁿ: c: V → C such that (u,v) ∈ E ⇒ c(u) ≠ c(v)

G = (V, E).

What is the smallest set of colours need to colour G?

Four Colour Theorem (for planar graphs)

So, for planar graphs, we can colour all vertices such that no pair of adjacent vertices with four colours (at max).

If the graph is non planar, there is no efficient algorithm known.

## Chromatic No.

Minimum No. of colours required to colour the whole graph.

- If a graph is circuit with n vertices then
  - it is 2-chromatic, if n is even.
  - it is 3-chromatic, if n is odd.


# Vertex Cover

→ Suppose, a hotel wants to install security cameras.

→ All corridors are straight lines.

→ Camera can monitor all corridors that meet at an intersection.

<img width="192" height="170" alt="image" src="https://github.com/user-attachments/assets/9b007b6a-ded4-49b3-bba5-563244ac7c6e" />

→ How many cameras needed (minimum)?

<img width="252" height="245" alt="image" src="https://github.com/user-attachments/assets/de0d8f87-9e13-4d4b-9fa8-e0773079905d" />

• So, if I put a camera on V₁ & V₂,
  all the corridors could be monitored.

∴ 2


# Independent Set

• A dance school puts up group dances.

Each dance has a set of dancers.

Set of dancers may overlap across dances.

V → Dances.
E → Set of dancers overlap.

Since, each dancer performs at most once.

Maximum no. of dance possible??

<img width="252" height="256" alt="image" src="https://github.com/user-attachments/assets/fb827821-9093-47fc-9349-5f888380688a" />

So, if we choose (V₄) → V₈, V₁, V₃ → should not overlap.

We can choose (V₅) → V₆ → (V₁, V₂) → already not scheduled.

Then we can choose (V₇) → (V₃, V₈, V₆) → already not scheduled.

We can choose (V₂) now.

∴ 1st day, V₂, V₄, V₅, V₇

2nd day → V₁, V₃, V₆, V₈.

∴ The max no. of dance possible is 4.

Independent Set: Subset of vertices such that no two are connected by an edge.


# Matching

Class projects can be done by one or two people.

If two people, they must be friends.

V → People
E → Friendship

<img width="287" height="165" alt="image" src="https://github.com/user-attachments/assets/91e1c2a1-4c3f-4312-bd36-8ffc317812f3" />


Find a good allocation of groups.

↳ G = (V, E) is an undirected graph.

↳ A matching is a subset M ⊆ E of mutually disjoint edges.

To find a good allocation of groups, find maximal matching in G.

So,

(V₀, V₂), (V₁, V₃) & (V₄, V₅).
