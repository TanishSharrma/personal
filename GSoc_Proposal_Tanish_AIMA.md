# Developing  Python Algorithms for AIMA Book (Pseudocode)

Tanish Sharrma, AIMA 2019


## Contact

| Name     | Tanish Sharrma                                         |
|----------|--------------------------------------------------------|
| Email    | tanishsharrma22@gmail.com                              |
| Mobile   | +91-7838063629 (WhatsApp as well)                      |
| LinkedIn | http://linkedIn.com/in/TanishSharrma                   |
| Github   | @TanishSharrma, https://github.com/TanishSharrma       |
| Samples  | https://github.com/TanishSharrma/PythonAlgorithms      |
| Resume   | http://tanish.ueuo.com/cv.pdf                          |

## INDEX

| S.No.    |                                         TOPIC                                        |
|----------|--------------------------------------------------------------------------------------|
|   1      | Abstract                                                                             |
|   2      | Motivation and Personal Statement                                                    |
|   3      | Coding Samples                                                                       |
|   4      | Project Timeline and Details                                                         |
|   5      | Previous Projects and Work Experience                                                |


## Abstract

For the upcoming 4th edition of "Artificial Intelligence: A Modern Approach", to finish implementing all the pseudocode algorithms in the book in Python. As described in the aima-pseudocode project, almost all of the algorithms from the 3rd edition are done, but there are some new ones in the upcoming 4th edition. To ensure that the code follows the pseudocode well, and also shows good style.

| **Intensity** |           **Involves**           |    **Mentors**    |
| ------------- | -------------------------------- |------------------ |
| Intermediate  | Python, Machine Learning & AI    | Pierre de Lacaze  |
                  
  
## Motivation and Personal Statement

I am currently pursuing a degree in Statistics (Mathematics) and Computers and have always found it fascinating and exciting to implement Statistical and Machine Learning tools and models to Computers. I believe that Google Summer of Code is the perfect opportunity for me to practically apply my knowledge and skills in a useful environment.

I have a lot of experience programming in Python and have won competitions solving questions and developing algorithms. I have a striong passion for teaching and have first hand experience with pseudocode as well.

I have been programming for over 12 years and have Machine Learning, Artificial Intelligence and CUDA experience as well. I have attended various conferences on GPU computing and am aware of the enormous potential it has. This summer, I will solely be focusing on Google Summer of Code and have no other commitments.

I have undertaken several classes in my college related to Mathematics, Statistics and Computing. I have profound interest in Game Theory and found ways to implement it in Python (Axelrod Lib Python).

For full details on my projects, courses undertaken, internships, projects and research papers, please refer to my Resume : http://tanish.ueuo.com.cv.pdf

## Coding Samples (Python):

Coding samples for Python can found on my github : https://github.com/TanishSharrma/PythonAlgorithms.

A couple of examples are demonstrated below :

### 1) Introduction to Binary Tree (Developed for teaching a college class) :

```python
'''

Introduction to Binary Tree and its transversing functions in Python.
Pre-requisites : The person should be well versed in basic Python, OOP and Recursion.
By Tanish Sharrma

'''

class Node:                     # Creating a class Node and defining it's functions
    def __init__(self, data):

        self.left = None        # Left Child of the Node (Empty on creation)
        self.right = None       # Right Child of the Node (Empty on creation)
        self.data = data

    # Insert Node by the method of recursion
    def insert(self, data):

        if self.data:               # To check whether the current Node is empty or not
            if data < self.data:    # If the Node is not empty, then if the data value < Node's Value, we move to its Left Child
                if self.left is None:
                    self.left = Node(data)
                else:
                    self.left.insert(data)
            elif data >= self.data:     # If the data value > Node's Value, we move to its Right Child
                if self.right is None:
                    self.right = Node(data)
                else:
                    self.right.insert(data)
        else:
            self.data = data            # If the node is empty, then we set this as our current Node.

    # Print the Tree (Method used : Recursion)
    def PrintTree(self):
        if self.left:
            self.left.PrintTree()
        print( self.data),
        if self.right:
            self.right.PrintTree()

        # Postorder traversal
        # Left ->Right -> Root
    def PostorderTraversal(self, root):
        res = []
        if root:
            res = self.PostorderTraversal(root.left)
            res = res + self.PostorderTraversal(root.right)
            res.append(root.data)
        return res

        # Preorder traversal
        # Root -> Left ->Right
    def PreorderTraversal(self, root):
        res = []
        if root:
            res.append(root.data)
            res = res + self.PreorderTraversal(root.left)
            res = res + self.PreorderTraversal(root.right)
        return res

        # Inorder traversal
        # Left -> Root -> Right
    def inorderTraversal(self, root):
        res = []
        if root:
            res = self.inorderTraversal(root.left)
            res.append(root.data)
            res = res + self.inorderTraversal(root.right)
        return res

    # Finding a node by starting at the root node and moving down the tree
    def findNode(self, n):
        root = self
        found = False
        while True:
            if root == None:
                break
            elif root.data == n:
                found = True
                break
            elif root.data > n:
                root = root.left
            else:
                root = root.right
        if found:
            return True
        else:
            return False

# Testing out functions

root = Node(27)     # Creating a new tree by setting the root Node
root.insert(14)     # Inserting Nodes into the tree
root.insert(35)
root.insert(10)
root.insert(19)
root.insert(31)
root.insert(42)
root.insert(11)

tran_1 = root.PostorderTraversal(root)   # Post Order Tree Traversal Left ->Right -> Root
tran_2 = root.PreorderTraversal(root)    # Pre Order Tree Traversal Root -> Left -> Right
tran_3 = root.inorderTraversal(root)     # In Order Tree Traversal Left -> Root -> Right

node_exists_1 = root.findNode(42)        # Finding the node with the value 42. Returns True
node_exists_2 = root.findNode(88)        # Finding the node with the value 88. Returns False
```

### 2) Solving a Medium Difficulty Level Question (Solved in a Hackathon Cometition) :

```python
'''
QUESTION :

Given an array of ints, is it possible to divide the ints into two groups, so that the sum of one group is a multiple
of 10, and the sum of the other group is odd. Every int must be in one group or the other. Write a recursive helper
 method that takes whatever arguments you like, and make the initial call to your recursive helper from splitOdd10().
 (No loops needed.)

splitOdd10([5, 5, 5]) → true
splitOdd10([5, 5, 6]) → false
splitOdd10([5, 5, 6, 1]) → true

'''

def find10(nums, target):
    if nums[0]>target:
        if len(nums)>1:
            return find10(nums[1:],target)
        else:
            return [-1]
    else:
        tt = target-nums[0]
        if tt == 0:
            return [nums[0]]
        if len(nums)<2:
            return [-1]
        else:
            q = find10(nums[1:],tt)
            if q[0] != -1:
                q.append(nums[0])
                return q
            else:
                return find10(nums[1:],target)

 # This function (find10) finds and returns array of numbers whose sum equals to the target. If no
 # such group is found, an array is returned with -1

def make10(nums):
    if len(nums)==0:
        return [-1]
    sum = 0
    for i in range(len(nums)):
        sum += nums[i]
    target = int((sum-(sum%10))/10)
    for x in range(1, target+1):
        a = find10(nums,x*10)
        if a[0] != -1:
            break
    if a[0]!=-1:
        for p in range(len(a)):
            id = nums.index(a[p])
            if id+1<len(nums):
                nums = nums[0:id] + nums[id+1:]
            else:
                nums = nums[0:id]
        return nums
    else:
        return [-1]

# This function (make10) first sums the array and then takes the Highest multiple of 10 (Hx) which is less than
# the sum of the array. It then loops the array x no of times by setting target as 10 and its multiples
# till the highest multiple (Hx). if a match is found at the lowest level, the numbers returned in the array
# from find10 are then removed and this new array is returned. The find10 numbers can also be added in the resultant
# array by adding return [nums,a]

def sumArray(nums):
    sum = 0
    for i in range(len(nums)):
        sum += nums[i]
    return sum

def splitOdd10(nums):
    if sumArray(nums)<10:
        if sumArray(nums)%2==1:
            return True
        else:
            return False
    arr = make10(nums)
    if arr[0] == -1:
        return False
    else :
        a = sumArray(arr)
        if a%2==1:
            return True
        else:
            return False

# Test Cases :

print (splitOdd10([5, 5, 5]))               # Returns True
print (splitOdd10([5,5,6]))                 # Returns False
print (splitOdd10([5, 5, 6, 1]))            # Returns True
print (splitOdd10([6, 5, 5, 1]))            # Returns True
print (splitOdd10([6, 5, 5, 1, 10]))        # Returns True
print (splitOdd10([6, 5, 5, 5, 1]))         # Returns False
print (splitOdd10([1]))                     # Returns True
print (splitOdd10([]))                      # Returns False
print (splitOdd10([10, 7, 5, 5]))           # Returns True
print (splitOdd10([10, 0, 5, 5]))           # Returns False
print (splitOdd10([10, 7, 5, 5, 2]))        # Returns True
print (splitOdd10([10, 7, 5, 5, 1]))        # Returns False
```        

## Project Timeline and Details

### **Community Bonding Period** : May 6th - May 27th 

Before the official time period begins, I plan to further study the previous verions of AIMA (Artificial Intelligence: A Modern Approach). During this period, under my mentor, I plan to :

  - Solve issues and bugs being brought up by the members of the community.
    
  - Learn about the requirements of the author.
    
  - Understand the procedure and code being followed in the previous editions.
    
  - Learn about the models, methods and algoritms explained in the book for better understanding of the coding style to be followed.
    
  - Study the previous AIMA GSoc projects


### Working Period : May 27th - August 19th

  - After understanding the work during the "Community Bonding period", start creating pull requests from the github repository and begin coding.
  
  - Implementing pseudocode for algorithms for easy and simple understand of functions.

  - All the work would be done in Python.
  
  - Coding and providing examples for Theoretical Machine Learning and Artificial Intelligence.
  
  - Ensuring very clear coding, commenting, and documentation writing skills and showcasing enthusiasm for helping other people by explaining things well.


## Other Projects and Work Experience

I have undertaken two technical internships, one as a Software Engineer and one as a Data Science Researcher. I have been programming and developing complex Algorithms in Python and Java for a few years now and have started undertaking projects in the field of Data Science, Machine Learning and Artificial Intelligence. During my Summer Internship in the previous year (As a Data Science Intern), I gained tremendous amount of experience and exposure and learned to implement my knowledge in a practical field. 

I am eager to learn and have worked on several Machine Learning and Artificial Intelligence projects as well. Namely, Image Classifier using Convolutional Neural Network (CNN), Machine Learning models for datasets provided on Kaggle, Basics of CUDA and GPU Computing etc.

I have undertaken substantial number of Mathematics and Computing classes and am ready to have first hand experience tackling real life issues with CuPy. Details of everything aforementioned are in my Resume : http://tanish.ueuo.com/cv.pdf

Looking forward to working on this project for the summers !
