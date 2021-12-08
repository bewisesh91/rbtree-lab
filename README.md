# Red-Black Tree 구현 노트

## Red-Black Tree 개요 ##
### Red-Black Tree란? ###
- Red-Black Tree is a self-balancing binary search tree in which each node contains an extra bit for denoting the color of the node, either red or black.
### Red-Black Tree 속성 ###
- A Red-Black Tree satisfies the following properties:
    - 1. Red/Black Property: Every node is colored, either red or black.
    - 2. Root Property: The root is black.
    - 3. Leaf Property: Every leaf (NIL) is black.
    - 4. Red Property: If a red node has children then, the children are always black.
    - 5. Depth Property: For each node, any simple path from this node to any of its descendant leaf has the same black-depth(the number of black nodes).
- The limitations put on the node colors ensure that any simple path from the root to a leaf is not more than twice as long as any other such path. It helps in maintaining the self-balancing property of the red-black tree.
- Each node has the following attributes: color, key, left child, right child, parent(except root node)
<p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/red-black-tree_0.png"  width="500" height="300"/></p>

## Red-Black Tree 주요 기능 ##
### 1) Inserting an element into a Red-Black Tree ###
- While inserting a new node, the new node is always inserted as a RED node. 
- This is because inserting a red node does not violate the depth property of a Red-Black Tree(No5).
- It is harder to fix the problem introduced by violating the depth property than any other problems. 
- After insertion of a new node, if the tree is violating the properties of the red-black tree then, we do the following algorithm.
    - Do the following until **_the parent of newNode p is RED._**
    - If p is the left child of grandParent(gP) of newNode, do the following.
        - Case (1)
            - A. If the color of the right child(uncle) of gP of newNode is RED, set the color of both the children of gP as BLACK and the color of gP as RED.
            - B. Assign gP to newNode.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-case1.1-red-black.png" width="600" height="300"/></p>
        - Case 2)
            - C. Else if newNode is the right child of p then, assign p to newNode.
            - D. Left-Rotate newNode.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-case2.1-red-black.png" width="400" height="300"/></p>
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-case-2.2-red-black.png" width="600" height="300"/></p>
        - Case 3)
            - E. Set color of p as BLACK and color of gP as RED.
            - F. Right-Rotate gP.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-case-3.1-red-black.png" width="600" height="300"/></p>
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-case-3.2-red-black.png" width="600" height="300"/></p>
    - Else, do the followings.
        - If the color of the left child of gP of z is RED, set the color of both the children of gP as BLACK and the color of gP as RED.
        - Assign gP to newNode.
        - Else if newNode is the left child of p then, assign p to newNode and Right-Rotate newNode.
        - Set color of p as BLACK and color of gP as RED.
        - Left-Rotate gP.
  - Set the root of the tree as BLACK.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-laststep-red-black.png" width="400" height="300"/></p>
  - The final tree looks like this.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/insertfix-final-tree-red-black.png" width="600" height="400"/></p>
  

### 2) Deleting an element into a Red-Black Tree ###
- Deleting a node may or may not disrupt the red-black properties of a Red-Black Tree. 
- If this action violates the red-black properties, then a fixing algorithm is used to regain the Red-Black properties.
    - Let the nodeToBeDeleted be
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-1-red-black.png" width="400" height="300"/></p>
    - Save the color of nodeToBeDeleted in origrinalColor.
    - If the left child of nodeToBeDeleted is NULL.
        - Assign the right child of nodeToBeDeleted to x.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-2-red-black.png" width="400" height="300"/></p>
        - Transplant nodeToBeDeleted with x.
            <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-3-red-black.png" width="600" height="300"/></p>
    - Else if the right child of nodeToBeDeleted is NULL
        - Assign the left child of nodeToBeDeleted into x.
        - Transplant nodeToBeDeleted with x.
    - Else
        - Assign the minimum of right subtree of noteToBeDeleted into y.
        - Save the color of y in originalColor.
        - Assign the rightChild of y into x.
        - If y is a child of nodeToBeDeleted, then set the parent of x as y.
        - Else, transplant y with rightChild of y.
        - Transplant nodeToBeDeleted with y.
        - Set the color of y with originalColor.
    - If the originalColor is BLACK, call the algorithm to maintain Red-Black property after deletion.
    - This algorithm is implemented when a black node is deleted because it violates the black depth property of the Red-Black Tree.
    - This violation is corrected by assuming that node x (which is occupying y's original position) has an extra black. 
    - This makes node x neither red nor black. It is either doubly black or black-and-red. 
    - This violates the Red-Black properties.
    - However, the color attribute of x is not changed rather the extra black is represented in x's pointing to the node.
    - The extra black can be removed if
        - 1) It reaches the root node.
        - 2) If x points to a red-black node. In this case, x is colored black.
        - 3) Suitable rotations and recolorings are performed.
    - Following algorithm retains the properties of a red-black tree.
    - Do the following until the x is not the root of the tree and the color of x is BLACK
    - If x is the left child of its parent then,
        - A. Assign w to the sibling of x.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-4-red-black.png" width="400" height="300"/></p>
        - B. If the sibling of x is RED,
        - Case (1)
            - Set the color of the right child of the parent of x as BLACK.
            - Set the color of the parent of x as RED.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-5-red-black.png" width="600" height="300"/></p>
            - Left-Rotate the parent of x.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-6-red-black.png" width="600" height="300"/></p>
            - Assign the rightChild of the parent of x to w.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-7-red-black.png" width="400" height="300"/></p>
        - C. If the color of both the right and the leftChild of w is BLACK,
        - Case (2)
            - Set the color of w as RED
            - Assign the parent of x to x.
        - D. Else if the color of the rightChild of w is BLACK
        - Case (3)
            - Set the color of the leftChild of w as BLACK
            - Set the color of w as RED
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-8-red-black.png" width="600" height="300"/></p>
            - Right-Rotate w.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-9-red-black.png" width="600" height="300"/></p>
            - Assign the rightChild of the parent of x to w.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-10-red-black.png" width="400" height="300"/></p>        
        - E. If any of the above cases do not occur, then do the following.
        - Case (4)
            - Set the color of w as the color of the parent of x.
            - Set the color of the parent of parent of x as BLACK.
            - Set the color of the right child of w as BLACK.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-11-red-black.png" width="600" height="300"/></p>
            - Left-Rotate the parent of x.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-12-red-black.png" width="600" height="300"/></p>
            - Set x as the root of the tree.
                <p align="center"><img src="https://cdn.programiz.com/sites/tutorial2program/files/delete-13-red-black.png" width="400" height="300"/></p>  
    - Else same as above with right changed to left and vice versa.
    -Set the color of x as BLACK.

# Red-Black Tree 구현

Balanced search tree로 많이 쓰이는 Red-black tree (이하 RB tree)를 C 언어로 구현해 보는 과제입니다.
구현하는 추상 자료형(abstract data type)은 ordered set, multiset 입니다.

## 구현 범위
다음 기능들을 수행할 수 있도록 RB tree를 구현합니다.

- tree = `new_tree()`: RB tree 구조체 생성 - 구현되어 있음
- `delete_tree(tree)`: RB tree 구조체가 차지했던 메모리 반환

- `tree_insert(tree, key)`: key 추가
- ptr = `tree_find(tree, key)`
    - RB tree내에 해당 key가 있는지 탐색하여 있으면 해당 node pointer 반환
    - 없으면 NIL 반환
- `tree_erase(tree, ptr)`: ptr로 지정된 node 삭제 및 메모리 반환
- ptr = `tree_min(tree)`: RB tree 중 최소 값을 가진 node pointer 반환
- ptr = `tree_max(tree)`: 최대값을 가진 node pointer 반환

- `tree_to_array(tree, array, n)`
  - RB tree의 내용을 *key 순서대로* 주어진 array로 변환
  - array의 크기는 n으로 주어지며 tree의 크기가 n 보다 큰 경우에는 순서대로 n개 까지만 변환

## 구현 규칙
- `src/rbtree.c` 이외에는 수정하지 않고 test를 통과해야 합니다.

## 과제의 의도 (Motivation)

- 복잡한 자료구조(data structure)를 구현해 봄으로써 자신감 상승
- C 언어, 특히 포인터(pointer)와 malloc, free 등의 system call에 익숙해짐.
- 동적 메모리 할당(dynamic memory allocation)을 직접 사용해 봄으로써 동적 메모리 할당의 필요성 체감 및 data segment에 대한 이해도 상승
- 고급 언어에서 기본으로 제공되는 자료구조가 세부적으로는 어떻게 구현되어 있는지 경험함으로써 고급 언어 사용시에도 효율성 고려

## 참고문헌
- [위키백과: 레드-블랙 트리](https://ko.wikipedia.org/wiki/%EB%A0%88%EB%93%9C-%EB%B8%94%EB%9E%99_%ED%8A%B8%EB%A6%AC)
([영어](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree))
- CLRS book (Introduction to Algorithms) 13장 레드 블랙 트리
- [Wikipedia:균형 이진 트리의 구현 방법들](https://en.wikipedia.org/wiki/Self-balancing_binary_search_tree#Implementations)
