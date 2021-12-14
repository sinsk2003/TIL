# 트리의 순회

- 노드를 특정한 방법으로 한 번씩 방문하는 방법

- 전위 순회(pre-order): 루트->왼쪽->오른쪽 
- 중위 순회(in-order): 왼쪽->루트->오른쪽
- 후위 순회(post-order): 왼쪽->오른쪽->루트

```python
class Node:
	def __init__(self, data, left_node, right_node):
        self.data = data
        self.left_node = left_node
        self.right_node = right_node

# 전위 순회(Preorder)
def pre_order(node):
    print(node.data, end = ' ')
    if node.left_node != None:
        pre_order(tree[Node.left_node])
    if node.right_node != None:
        pre_order(tree[Node.right_node])

# 중위 순회(Inorder)
def in_order(node):
    if node.left_node != None:
        in_order(tree[Node.left_node])
    print(node.data, end = ' ')
    if node.right_node != None:
        in_order(tree[Node.right_node])
        
# 후위 순회(Postorder)
def post_order(node):
    if node.left_node != None:
        post_order(tree[Node.left_node])
    if node.right_node != None:
        post_order(tree[Node.right_node])
    print(node.data, end = ' ')
    
n = int(input())
tree = {}

for i in range(n):
    daa, left_node, right_node = input().split()
    if left_node == "None":
        left_node == None
    if right_node == "None":
       	right_node == None
    tree[data] = Node(data, left_node, right_node)
    
pre_order(tree['A'])
print()
in_order(tree['A'])
print()
post_order(tree['A'])
```

