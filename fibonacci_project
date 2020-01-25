import math
# Creating a Fibonacci Heap

class Fibo:


	class Node:


		def __init__(self, key, value):

			self.key    = key
			self.value  = value
			self.child  = None
			self.parent = None
			self.left   = None
			self.right  = None
			self.min    = None			
			self.p      = None
			self.child  = None
			self.degree = 0
			self.mark   = False


	def loop(self, head):
		node = head
		stop = head
		flag = False
		while True:
			if node == stop and flag is True:	
				break
			elif node == stop:
				flag = True
			yield node
			node = node.right

	root_list = None
	min_node  = None

	total_nodes = 0

	def Min(self):
		return self.min_node

	def extract_min(self):
		z = self.min_node
		if z is not None:
			if z.child is not None:
				children = [x for x in self.loop(z.child)]
				for i in range(0, len(children)):
					self.root_insert(children[i])
					children[i].parent = None
			self.root_remove(z)

			if z == z.right:
				self.min_node = self.root_list = None
			else:
				self.min_node = z.right
				self.consolidate()
			self.total_nodes -= 1
		return z


		
	def root_insert(self,node):
	
		if self.root_list is None:
			self.root_list = node
		else:
			node.right = self.root_list.right
			node.left = self.root_list
			self.root_list.right.left = node
			self.root_list.right = node
	
	
	
	def fib_insert(self,key,value= None):

		val = self.Node(key, value)
		val.right = val
		val.left  = val
		self.root_insert(val)
		if self.min_node is None or val.key < self.min_node.key:
			self.min_node = val
		self.total_nodes += 1
		return val

	def dec_key(self,x , k):
		if k > x.key:
			return None
		x.key = k
		y = x.parent
		if y is not None and x.key < y.key:

			self.cut(x , y)
			self.cascading_cut(y)
		if x.key < self.min_node.key:	
			self.min_node = x
	def union(self, var):

		N = Fibo()
		N.root_list, N.min_node = self.root_list , self.min_node
		
		last = var.root_list.left
		N.root_list.left.right = var.root_list
		N.root_list.left = last
		N.root_list.left.right= N.root_list

		if var.min_node.key < N.min_node.key:
			N.min_node = var.min_node

		N.total_nodes = self.total_nodes + var.total_nodes
		return N


	def cut(self,x , y):

		self.remove_child_list( y , x)
		y.degree -= 1
		self.root_insert(x)
		x.parent = None
		x.mark   = False

	def flow_cut(self, y):
		item = y.parent
		if  not ( item is None):
			if y.mark is False:
				y.mark = True
			else:
				self.cut(y , item)
				self.flow_cut(item)		
	def consolidate(self):
			
		A = [None] * int(math.log(self.total_nodes) * 2)
		nodes = [w for w in self.loop(self.root_list)]
		for w in range(0, len(nodes)):
			x = nodes[w]
			d = x.degree
			while A[d] != None:
				y = A[d]
				if x.key > y.key:
					temp = x
					x,y = y, temp
				self.heap_link(y , x)
				A[d] = None
				d += 1
			A[d] = x


		for i in range(0,len(A)):
			if A[i] is not None:
				if A[i].key < self.min_node.key:
					self.min_node = A[i]


	def heap_link(self, y, x):
		self.root_remove(y)
		y.left  = y
		y.right = y
		self.child_insert(x, y)
		x.degree += 1
		y.parent= x
		y.mark  = False

	def child_insert(self,parent, node):

		if parent.child is None:
			parent.child = node
		else:
			node.right = parent.child.right
			node.left = parent.child
			parent.child.right.left = node
			parent.child.right = node



	def root_remove(self,node):
		if node == self.root_list:
			self.root_list = node.right
		node.left.right = node.right
		node.right.left = node.left


	def child_remove(self,parent,node):

		if parent.child == parent.child.right:
			parent.child = None
		elif parent.child == node:
			parent.child = node.right
			node.right.parent = parent
		node.left.right = node.right
		node.right.left = node.left





	
			
n = Fibo()
n.fib_insert(10)
n.fib_insert(2)
n1 = Fibo()
n1.fib_insert(15)
n1.fib_insert(6)
n.Min()
n.extract_min()
f3 = n.union(n1)

