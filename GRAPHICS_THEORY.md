# Theory of some important topics

## Scene graph
In Three.js, a scene graph is a hierarchical data structure used to organize and manage all the objects in a 3D scene.

At its core, s scene graph is like a tree structure, where:

- The root is the `Scene` object.
- Each node is an `Object3D` (or a subclass like `Mesh`, `Group`, `Camera`, `Light`, etc.).
- You add things as child using `.add()` method. 
```
Ex. scene.add(camera);
Ex. carGeometry.add(playerGeometry)
```
- Each node can have children, forming a parent-child relationship.

### Why it's important:
The scene graph lets you:

- Organize complex scenes easily.
- Apply transformations (position, rotation, scale) to parent objects and have them affect all children.
- Efficiently render scenes by traversing the graph and drawing each object.