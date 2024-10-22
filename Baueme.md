# Binärbaum in Java



Zwei der wichtigsten Themen in der Informatik sind das **Sortieren** und **Suchen** von Datensätzen. Eine Datenstruktur, die für beides häufig verwendet wird, ist der **Binärbaum**. In diesem Artikel lernst du:

- Was ist ein Binärbaum?
- Welche Arten von Binärbäumen gibt es?
- Wie implementiert man einen Binärbaum in Java?
- Welche Operationen stellen Binärbäume bereit?
- Was bedeuten **pre-order**, **in-order**, **post-order** und **level-order** bei der Traversierung?

### Was ist ein Binärbaum?

Ein **Binärbaum** ist eine Baum-Datenstruktur, in der jeder Knoten maximal zwei Kindknoten hat. Diese Kindknoten werden als **linkes** und **rechtes Kind** bezeichnet.

### Binärbaum-Arten

- **Voller Binärbaum**: Jeder Knoten hat entweder keine oder zwei Kinder.
- **Kompletter Binärbaum**: Alle Ebenen, außer der letzten, sind vollständig gefüllt.
- **Perfekter Binärbaum**: Ein voller Binärbaum, in dem alle Blätter die gleiche Tiefe haben.
- **Balancierter Binärbaum**: Die Höhe der linken und rechten Teilbäume jedes Knotens unterscheidet sich um maximal eins.
- **Sortierter Binärbaum**: Der linke Teilbaum enthält Werte, die kleiner oder gleich dem Elternknoten sind, der rechte Teilbaum enthält Werte, die größer oder gleich sind.

### Implementierung in Java

Die Knoten des Binärbaums können mit der folgenden **Java-Klasse** implementiert werden:

```java
public class Node {
  int data;
  Node left;
  Node right;
  Node parent;

  public Node(int data) {
    this.data = data;
  }
}
```

Der Binärbaum selbst enthält eine Referenz auf den Wurzelknoten:

```java
public interface BinaryTree {
  Node getRoot();
}

public class BaseBinaryTree implements BinaryTree {
  Node root;

  @Override
  public Node getRoot() {
    return root;
  }
}
```

### Traversierung eines Binärbaums

Eine wichtige Operation bei Binärbäumen ist die **Traversierung**, also das Besuchen aller Knoten in einer bestimmten Reihenfolge:

- **Pre-Order (N-L-R)**: Besucht den aktuellen Knoten, dann den linken und rechten Teilbaum.
- **Post-Order (L-R-N)**: Besucht zuerst die Teilbäume und dann den aktuellen Knoten.
- **In-Order (L-N-R)**: Besucht den linken Teilbaum, dann den aktuellen Knoten und danach den rechten Teilbaum.
- **Level-Order**: Besucht die Knoten Ebene für Ebene von links nach rechts.

Beispielcode für eine Pre-Order-Traversierung:

```java
public static void traversePreOrder(Node node, NodeVisitor visitor) {
  if (node == null) {
    return;
  }
  visitor.visit(node);
  traversePreOrder(node.left, visitor);
  traversePreOrder(node.right, visitor);
}
```

### Beispiel: Einfügen und Traversieren eines Binärbaums in Java

Hier ist ein vollständiges Beispiel, das das Einfügen und Traversieren eines Binärbaums in Java zeigt:

```java
public class BinaryTreeExample {
  public static void main(String[] args) {
    BaseBinaryTree tree = new BaseBinaryTree();
    tree.root = new Node(10);

    // Füge Knoten ein
    Node leftChild = insertNode(5, tree.root, Side.LEFT);
    Node rightChild = insertNode(15, tree.root, Side.RIGHT);
    insertNode(3, leftChild, Side.LEFT);
    insertNode(7, leftChild, Side.RIGHT);
    insertNode(13, rightChild, Side.LEFT);
    insertNode(18, rightChild, Side.RIGHT);

    // Traversiere den Baum in Pre-Order
    traversePreOrder(tree.getRoot(), new NodeVisitor() {
      @Override
      public void visit(Node node) {
        System.out.print(node.data + " ");
      }
    });
  }

  public static Node insertNode(int data, Node parent, Side side) {
    var node = new Node(data);
    node.parent = parent;
    switch (side) {
      case LEFT -> {
        if (parent.left != null) {
          node.left = parent.left;
          node.left.parent = node;
        }
        parent.left = node;
      }
      case RIGHT -> {
        if (parent.right != null) {
          node.right = parent.right;
          node.right.parent = node;
        }
        parent.right = node;
      }
      default -> throw new IllegalStateException();
    }
    return node;
  }

  public static void traversePreOrder(Node node, NodeVisitor visitor) {
    if (node == null) {
      return;
    }
    visitor.visit(node);
    traversePreOrder(node.left, visitor);
    traversePreOrder(node.right, visitor);
  }

  interface NodeVisitor {
    void visit(Node node);
  }

  enum Side {
    LEFT, RIGHT
  }
}
```

### Operationen auf Binärbäumen

Neben der Traversierung sind die grundlegenden Operationen auf Binärbäumen das **Einfügen** und **Löschen** von Knoten. Der Code für das Einfügen eines neuen Knotens kann wie folgt aussehen:

```java
public Node insertNode(int data, Node parent, Side side) {
  var node = new Node(data);
  node.parent = parent;
  switch (side) {
    case LEFT -> {
      if (parent.left != null) {
        node.left = parent.left;
        node.left.parent = node;
      }
      parent.left = node;
    }
    case RIGHT -> {
      if (parent.right != null) {
        node.right = parent.right;
        node.right.parent = node;
      }
      parent.right = node;
    }
    default -> throw new IllegalStateException();
  }
  return node;
}
```

### Array-Darstellung eines Binärbaums

Ein Binärbaum kann auch als **Array** gespeichert werden. Die Knoten werden von der Wurzel abwärts, Ebene für Ebene, von links nach rechts durchnummeriert.

### Zusammenfassung

Ein **Binärbaum** ist eine vielseitige Datenstruktur, die zum Sortieren und Suchen von Daten verwendet wird. Dieser Artikel behandelt die verschiedenen **Arten von Binärbäumen**, deren **Traversierungen** sowie die **Implementierung in Java**.

Mehr Informationen und den vollständigen Quellcode findest du auf [GitHub](https://github.com/HappyCodersEU/Binaerbaum).

