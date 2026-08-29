# Real-World Network Analysis - Social Network

n = int(input("Enter number of people: "))

# Accept vertices
people = []
for i in range(n):
    name = input(f"Enter person {i + 1}: ")
    people.append(name)

# Choose graph type
choice = input("Enter graph type (D for Directed / U for Undirected): ").upper()

# Create adjacency list
graph = {person: [] for person in people}

# Accept connections
e = int(input("Enter number of connections: "))

for i in range(e):
    print(f"\nConnection {i + 1}")
    person1 = input("Enter first person: ")
    person2 = input("Enter second person: ")

    graph[person1].append(person2)

    # For undirected graph, add both directions
    if choice == "U":
        graph[person2].append(person1)

# Display vertices
print("\n--- Vertices ---")
for person in people:
    print(person)

# Display edges
print("\n--- Edges ---")
for person in people:
    for neighbour in graph[person]:
        print(person, "->", neighbour)

# Display neighbours
print("\n--- Neighbours ---")
for person in people:
    print(person, ":", graph[person])

# Find node with maximum connections
max_node = people[0]

for person in people:
    if len(graph[person]) > len(graph[max_node]):
        max_node = person

print("\n--- Maximum Connections ---")
print("Person with maximum connections:", max_node)
print("Number of connections:", len(graph[max_node]))
