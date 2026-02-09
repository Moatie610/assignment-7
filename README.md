# Team Management Tree

You've joined the internal tools team at a growing tech company. The leadership team wants an interactive tool to visualize how employees report to one another. Some employees manage others, and some only report to a single manager. The company wants a structure that can grow as the team scales.

Instead of using a flat list or table, you're tasked with building a **custom binary tree** that represents this hierarchy. Each employee can have up to two direct reports, and you’ll need to build this system using recursive insertion and traversal.

Your program should run in the terminal and allow users to:

- Add a root team lead (CEO or equivalent)
- Add new employees under a specific manager (left or right)
- Print the current reporting structure as a tree

This assignment builds your understanding of **binary trees**, recursive insertion, and tree traversal. These skills are foundational not just for technical interviews, but also for modeling complex, real-world relationships like file systems, routing hierarchies, and decision paths.

## Classes

### `EmployeeNode` Class
Represents a single employee in the tree.

**Constructor**

```python
EmployeeNode(name)
```

**Attributes**
- `name` (str): The employee's name.
- `left` (`EmployeeNode` or `None`): Points to the employee's left report.
- `right` (`EmployeeNode` or `None`): Points to the employee's right report.

### `TeamTree` Class
Manages the full team reporting structure.

**Constructor**

```python
TeamTree()
```
**Attributes**
- `root` (`EmployeeNode` or `None`): The top-most employee in the organization.

**Methods**

`insert(manager_name: str, employee_name: str, side: str) -> None`
- Recursively searches for `manager_name`.
- Adds `employee_name` as the `left` or `right` child based on the side argument.
- Prints a helpful success or error message.

`print_tree(node: EmployeeNode or None = None, level: int = 0) -> None`
- Recursively prints the current team structure from top to bottom.
- Visually indents based on hierarchy level.
- Defaults to printing from the root.

class EmployeeNode:
    """
    Represents a single employee in the company tree.
    Each employee can have up to two direct reports (left and right).
    """

    def __init__(self, name):
        self.name = name
        self.left = None
        self.right = None


class TeamTree:
    """
    Manages the full company reporting structure using a binary tree.
    """

    def __init__(self):
        self.root = None

    # ---------- Recursive Insert ----------
    def insert(self, manager_name, employee_name, side, current_node=None):

        # Start at root if first call
        if current_node is None:
            current_node = self.root

        # If tree is empty
        if current_node is None:
            print("❌ No team lead exists. Add a root first.")
            return

        # Found the manager
        if current_node.name == manager_name:

            if side.lower() == "left":
                if current_node.left is None:
                    current_node.left = EmployeeNode(employee_name)
                    print(f"✅ {employee_name} added to the LEFT of {manager_name}")
                else:
                    print("❌ Left side already occupied.")

            elif side.lower() == "right":
                if current_node.right is None:
                    current_node.right = EmployeeNode(employee_name)
                    print(f"✅ {employee_name} added to the RIGHT of {manager_name}")
                else:
                    print("❌ Right side already occupied.")

            else:
                print("❌ Side must be 'left' or 'right'.")
            return

        # Search left subtree
        if current_node.left:
            self.insert(manager_name, employee_name, side, current_node.left)

        # Search right subtree
        if current_node.right:
            self.insert(manager_name, employee_name, side, current_node.right)

    # ---------- Recursive Print ----------
    def print_tree(self, node=None, level=0):_
