**1.** **Stack** **Push** **and** **Pop** **(using** **array** **VLA)**

\#include \<iostream\> using namespace std;

int main() { int size;

> cout \<\< "Enter stack capacity: "; cin \>\> size;
>
> int stack\[size\]; int top = -1;
>
> int choice, value; while (true) {
>
> cout \<\< "1. Push\n2. Pop\n3. Exit\nEnter choice: "; cin \>\> choice;
>
> if (choice == 1) {
>
> if (top \>= size - 1) {
>
> cout \<\< "Stack overflow!\n"; } else {
>
> cout \<\< "Enter value to push: "; cin \>\> value;
>
> stack\[++top\] = value; }
>
> } else if (choice == 2) { if (top \< 0) {
>
> cout \<\< "Stack underflow!\n"; } else {
>
> cout \<\< "Popped: " \<\< stack\[top--\] \<\< endl; }
>
> } else if (choice == 3) { break;
>
> } else {
>
> cout \<\< "Invalid choice!\n"; }
>
> }

return 0; }

**2.** **Balanced** **Parentheses** **(with** **\[\],** **{})**

\#include \<iostream\> \#include \<vector\> \#include \<string\> using
namespace std;

int main() { string expr;

> cout \<\< "Enter expression: "; cin \>\> expr;
>
> vector\<char\> st; bool ok = true;
>
> for (char c : expr) {
>
> if (c=='('\|\|c=='\['\|\|c=='{') { st.push_back(c);
>
> } else if (c==')'\|\|c=='\]'\|\|c=='}') {
>
> if (st.empty()) { ok = false; break; } char t = st.back();
> st.pop_back();
>
> if ((c==')'&&t!='(') \|\| (c=='\]'&&t!='\[') \|\| (c=='}'&&t!='{')) {
> ok = false; break;
>
> } }
>
> }
>
> if (!st.empty()) ok = false;
>
> cout \<\< (ok ? "Balanced!" : "Unbalanced!") \<\< endl; return 0;

}

**3.** **Queue** **Using** **Two** **Stacks**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { vector\<int\> s1, s2; int choice, value; while (true) {

> cout \<\< "1. Enqueue\n2. Dequeue\n3. Exit\nEnter choice: "; cin \>\>
> choice;
>
> if (choice == 1) {
>
> cout \<\< "Enter value: "; cin \>\> value; s1.push_back(value);
>
> } else if (choice == 2) { if (s2.empty()) {
>
> while (!s1.empty()) { s2.push_back(s1.back()); s1.pop_back();
>
> } }
>
> if (!s2.empty()) {
>
> cout \<\< "Dequeued: " \<\< s2.back() \<\< endl; s2.pop_back();
>
> } else {
>
> cout \<\< "Queue empty!" \<\< endl; }
>
> } else if (choice == 3) { break;
>
> } }

return 0; }

**4.** **Queue** **Front** **and** **Rear** **(efficient)**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() {

> int n = 1000; // max capacity vector\<int\> q(n);
>
> int head = 0, tail = 0; int choice, value; while (true) {
>
> cout \<\< "1. Enqueue\n2. Dequeue\n3. Front\n4. Rear\n5. Exit\nEnter
> choice: "; cin \>\> choice;
>
> if (choice == 1) {
>
> cout \<\< "Enter value: "; cin \>\> value;
>
> if ((tail + 1) % n == head) { cout \<\< "Queue Full!" \<\< endl;
>
> } else {
>
> q\[tail\] = value;
>
> tail = (tail + 1) % n; }
>
> } else if (choice == 2) { if (head == tail) {
>
> cout \<\< "Queue Empty!" \<\< endl; } else {
>
> cout \<\< "Dequeued: " \<\< q\[head\] \<\< endl; head = (head + 1) %
> n;
>
> }
>
> } else if (choice == 3) {
>
> if (head == tail) cout \<\< "Queue Empty!" \<\< endl; else cout \<\<
> "Front: " \<\< q\[head\] \<\< endl;
>
> } else if (choice == 4) {
>
> if (head == tail) cout \<\< "Queue Empty!" \<\< endl;
>
> else cout \<\< "Rear: " \<\< q\[(tail - 1 + n) % n\] \<\< endl; } else
> if (choice == 5) {
>
> break; }
>
> }

return 0; }

**5.** **Count** **Nodes** **in** **Linked** **List**

\#include \<iostream\> using namespace std;

struct Node { int data; Node\* next; };

int main() { int n, v;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> Node\* head = nullptr;
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\> v;
>
> Node\* node = new Node{v, head}; head = node;
>
> }
>
> int cnt = 0; Node\* cur = head; while (cur) {
>
> cnt++;
>
> cur = cur-\>next; }
>
> cout \<\< "Total nodes: " \<\< cnt \<\< endl; return 0;

}

**6.** **Detect** **Cycle** **in** **Linked** **List**

\#include \<iostream\> using namespace std;

struct Node { int data; Node\* next; };

int main() {

> int n, v, pos;
>
> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> Node\* head = nullptr;
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\> v;
>
> Node\* node = new Node{v, head}; head = node;
>
> }
>
> cout \<\< "Enter position (0-based) to link tail for cycle, or -1 for
> none: "; cin \>\> pos;
>
> if (pos \>= 0) {
>
> Node\* tail = head;
>
> while (tail-\>next) tail = tail-\>next; Node\* target = head;
>
> for (int i = 0; i \< pos; ++i) target = target-\>next; tail-\>next =
> target;
>
> }
>
> Node\* slow = head; Node\* fast = head; bool cycle = false;
>
> while (fast && fast-\>next) { slow = slow-\>next;
>
> fast = fast-\>next-\>next;
>
> if (slow == fast) { cycle = true; break; } }
>
> cout \<\< (cycle ? "Cycle detected!" : "No cycle detected!") \<\<
> endl; return 0;

}

**7.** **Reverse** **Linked** **List**

\#include \<iostream\> using namespace std;

struct Node { int data; Node\* next; };

int main() { int n, v;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> Node\* head = nullptr;
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\> v;
>
> Node\* node = new Node{v, head}; head = node;
>
> }
>
> Node\* prev = nullptr; Node\* curr = head; while (curr) {
>
> Node\* nxt = curr-\>next; curr-\>next = prev; prev = curr;
>
> curr = nxt; }
>
> head = prev;
>
> cout \<\< "Reversed list: "; Node\* p = head;
>
> while (p) {
>
> cout \<\< p-\>data \<\< " "; p = p-\>next;
>
> }
>
> cout \<\< endl; return 0;

}

**8.** **Bubble** **Sort**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> for (int i = 0; i \< n - 1; ++i) {
>
> for (int j = 0; j \< n - 1 - i; ++j) {
>
> if (a\[j\] \> a\[j+1\]) swap(a\[j\], a\[j+1\]); }
>
> }
>
> cout \<\< "Sorted: ";
>
> for (int x : a) cout \<\< x \<\< " "; cout \<\< endl;

return 0; }

**9.** **Selection** **Sort**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> for (int i = 0; i \< n - 1; ++i) { int mi = i;
>
> for (int j = i+1; j \< n; ++j) { if (a\[j\] \< a\[mi\]) mi = j;
>
> }
>
> swap(a\[i\], a\[mi\]); }
>
> cout \<\< "Sorted: ";
>
> for (int x : a) cout \<\< x \<\< " "; cout \<\< endl;

return 0; }

**10.** **Insertion** **Sort**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> for (int i = 1; i \< n; ++i) { int key = a\[i\], j = i - 1;
>
> while (j \>= 0 && a\[j\] \> key) { a\[j+1\] = a\[j\];
>
> j--; }
>
> a\[j+1\] = key; }
>
> cout \<\< "Sorted: ";
>
> for (int x : a) cout \<\< x \<\< " "; cout \<\< endl;

return 0; }

**11.** **Quick** **Sort** **(inline)**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> vector\<pair\<int,int\>\> stk; stk.push_back(make_pair(0, n-1)); while
> (!stk.empty()) {
>
> auto range = stk.back(); stk.pop_back(); int low = range.first, high =
> range.second; if (low \>= high) continue;
>
> int pivot = a\[high\], i = low-1; for (int j = low; j \< high; ++j) {
>
> if (a\[j\] \<= pivot) swap(a\[++i\], a\[j\]); }
>
> swap(a\[i+1\], a\[high\]); int p = i+1;
>
> stk.push_back(make_pair(low, p-1)); stk.push_back(make_pair(p+1,
> high));
>
> }
>
> cout \<\< "Sorted: ";
>
> for (int x : a) cout \<\< x \<\< " "; cout \<\< endl;

return 0; }

**12.** **Merge** **Sort** **(iterative)**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n), tmp(n); for (int i = 0; i \< n; ++i) {
>
> cout \<\< "Enter value: "; cin \>\> a\[i\];
>
> }
>
> for (int sz = 1; sz \< n; sz \*= 2) { for (int l = 0; l \< n; l +=
> 2\*sz) {
>
> int m = min(l+sz, n), r = min(l+2\*sz, n); int i = l, j = m, k = l;
>
> while (i \< m && j \< r) {
>
> if (a\[i\] \<= a\[j\]) tmp\[k++\] = a\[i++\]; else tmp\[k++\] =
> a\[j++\];
>
> }
>
> while (i \< m) tmp\[k++\] = a\[i++\]; while (j \< r) tmp\[k++\] =
> a\[j++\];
>
> for (int t = l; t \< r; ++t) a\[t\] = tmp\[t\]; }
>
> }
>
> cout \<\< "Sorted: ";
>
> for (int x : a) cout \<\< x \<\< " "; cout \<\< endl;

return 0; }

**13.** **Linear** **Search**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n, key;

> cout \<\< "Enter number of elements: "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> cout \<\< "Enter element to search: "; cin \>\> key;
>
> int idx = -1;
>
> for (int i = 0; i \< n; ++i) {
>
> if (a\[i\] == key) { idx = i; break; } }
>
> if (idx != -1) cout \<\< "Found at index " \<\< idx \<\< endl; else
> cout \<\< "Not found" \<\< endl;

return 0; }

**14.** **Binary** **Search**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n, key;

> cout \<\< "Enter number of elements (sorted): "; cin \>\> n;
>
> vector\<int\> a(n);
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\>
> a\[i\];
>
> }
>
> cout \<\< "Enter element to search: "; cin \>\> key;
>
> int l = 0, r = n-1, idx = -1; while (l \<= r) {
>
> int m = l + (r - l) / 2;
>
> if (a\[m\] == key) { idx = m; break; } else if (a\[m\] \< key) l = m +
> 1; else r = m - 1;
>
> }
>
> if (idx != -1) cout \<\< "Found at index " \<\< idx \<\< endl; else
> cout \<\< "Not found" \<\< endl;

return 0; }

**15.** **Height** **of** **BST** **(user-built)**

\#include \<iostream\> \#include \<vector\> using namespace std;

struct Node { int data; Node\* left; Node\* right; };

int main() { int n, v;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> Node\* root = nullptr;
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\> v;
>
> Node\* cur = root; Node\* parent = nullptr; while (cur) {
>
> parent = cur;
>
> if (v \< cur-\>data) cur = cur-\>left; else cur = cur-\>right;
>
> }
>
> Node\* node = new Node{v, nullptr, nullptr}; if (!parent) root = node;
>
> else if (v \< parent-\>data) parent-\>left = node; else parent-\>right
> = node;
>
> }
>
> vector\<Node\*\> q;
>
> int head = 0, height = 0; if (root) q.push_back(root);
>
> while (head \< (int)q.size()) { int sz = q.size() - head; while (sz--)
> {
>
> Node\* t = q\[head++\];
>
> if (t-\>left) q.push_back(t-\>left); if (t-\>right)
> q.push_back(t-\>right);
>
> } height++;
>
> }
>
> cout \<\< "Height: " \<\< height \<\< endl; return 0;

}

**16.** **Count** **Nodes** **in** **BST** **(user-built)**

\#include \<iostream\> \#include \<vector\> using namespace std;

struct Node { int data; Node\* left; Node\* right; };

int main() { int n, v;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> Node\* root = nullptr;
>
> for (int i = 0; i \< n; ++i) { cout \<\< "Enter value: "; cin \>\> v;
>
> Node\* cur = root; Node\* parent = nullptr; while (cur) {
>
> parent = cur;
>
> if (v \< cur-\>data) cur = cur-\>left; else cur = cur-\>right;
>
> }
>
> Node\* node = new Node{v, nullptr, nullptr}; if (!parent) root = node;
>
> else if (v \< parent-\>data) parent-\>left = node; else parent-\>right
> = node;
>
> }
>
> vector\<Node\*\> q;
>
> int head = 0, cnt = 0;
>
> if (root) q.push_back(root); while (head \< (int)q.size()) {
>
> Node\* t = q\[head++\]; cnt++;
>
> if (t-\>left) q.push_back(t-\>left); if (t-\>right)
> q.push_back(t-\>right);
>
> }
>
> cout \<\< "Total nodes: " \<\< cnt \<\< endl; return 0;

}

**17.** **BFS** **on** **Graph**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n, m;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> cout \<\< "Enter number of edges: "; cin \>\> m;
>
> vector\<vector\<int\>\> adj(n);
>
> for (int i = 0, u, v; i \< m; ++i) { cout \<\< "Enter edge (u v): ";
> cin \>\> u \>\> v; adj\[u\].push_back(v); adj\[v\].push_back(u);
>
> }
>
> vector\<bool\> vis(n, false); vector\<int\> q;
>
> int head = 0, start;
>
> cout \<\< "Enter starting node: "; cin \>\> start;
>
> vis\[start\] = true; q.push_back(start); cout \<\< "BFS: ";
>
> while (head \< (int)q.size()) { int u = q\[head++\];
>
> cout \<\< u \<\< " ";
>
> for (int v : adj\[u\]) {
>
> if (!vis\[v\]) { vis\[v\] = true; q.push_back(v); } }
>
> }
>
> cout \<\< endl; return 0;

}

**18.** **DFS** **on** **Graph**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n, m;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> cout \<\< "Enter number of edges: "; cin \>\> m;
>
> vector\<vector\<int\>\> adj(n);
>
> for (int i = 0, u, v; i \< m; ++i) { cout \<\< "Enter edge (u v): ";
> cin \>\> u \>\> v; adj\[u\].push_back(v); adj\[v\].push_back(u);
>
> }
>
> vector\<bool\> vis(n, false); vector\<int\> stk;
>
> int start;
>
> cout \<\< "Enter starting node: "; cin \>\> start;
> stk.push_back(start);
>
> cout \<\< "DFS: "; while (!stk.empty()) {
>
> int u = stk.back(); stk.pop_back(); if (vis\[u\]) continue;
>
> vis\[u\] = true; cout \<\< u \<\< " ";
>
> for (int i = adj\[u\].size() - 1; i \>= 0; --i) { int v =
> adj\[u\]\[i\];
>
> if (!vis\[v\]) stk.push_back(v); }
>
> }
>
> cout \<\< endl; return 0;

}

**19.** **Graph** **Adj** **List** **&** **Matrix**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int n, m;

> cout \<\< "Enter number of nodes: "; cin \>\> n;
>
> cout \<\< "Enter number of edges: "; cin \>\> m;
>
> vector\<vector\<int\>\> list(n), mat(n, vector\<int\>(n, 0)); for (int
> i = 0, u, v; i \< m; ++i) {
>
> cout \<\< "Enter edge (u v): "; cin \>\> u \>\> v;
> list\[u\].push_back(v); list\[v\].push_back(u); mat\[u\]\[v\] =
> mat\[v\]\[u\] = 1;
>
> }
>
> cout \<\< "Adj List:\n";
>
> for (int i = 0; i \< n; ++i) { cout \<\< i \<\< ": ";
>
> for (int v : list\[i\]) cout \<\< v \<\< " "; cout \<\< "\n";
>
> }
>
> cout \<\< "Adj Matrix:\n";
>
> for (int i = 0; i \< n; ++i) {
>
> for (int j = 0; j \< n; ++j) cout \<\< mat\[i\]\[j\] \<\< " "; cout
> \<\< "\n";
>
> }

return 0; }

**20.** **Hash** **Table** **(with** **tombstones)**

\#include \<iostream\> \#include \<vector\> using namespace std;

int main() { int size;

> cout \<\< "Enter table size: "; cin \>\> size;
>
> vector\<int\> table(size, -1); const int DELETED = -2; while (true) {
>
> cout \<\< "1.Insert 2.Search 3.Remove 4.Exit\nChoice: "; int choice,
> key;
>
> cin \>\> choice;
>
> if (choice == 4) break; cout \<\< "Enter key: "; cin \>\> key;
>
> int idx = key % size; if (choice == 1) {
>
> int start = idx; bool inserted = false; do {
>
> if (table\[idx\] == -1 \|\| table\[idx\] == DELETED) { table\[idx\] =
> key;
>
> cout \<\< "Inserted at " \<\< idx \<\< endl; inserted = true; break;
>
> }
>
> idx = (idx + 1) % size; } while (idx != start);
>
> if (!inserted) cout \<\< "Table full!" \<\< endl; } else if (choice ==
> 2) {
>
> int start = idx, found = 0; do {
>
> if (table\[idx\] == key) { cout \<\< "Found at " \<\< idx \<\< endl;
> found = 1; break; } if (table\[idx\] == -1) break;
>
> idx = (idx + 1) % size; } while (idx != start);
>
> if (!found) cout \<\< "Not found" \<\< endl; } else if (choice == 3) {
>
> int start = idx, removed = 0; do {
>
> if (table\[idx\] == key) { table\[idx\] = DELETED;
>
> cout \<\< "Removed from " \<\< idx \<\< endl; removed = 1; break;
>
> }
>
> if (table\[idx\] == -1) break; idx = (idx + 1) % size;
>
> } while (idx != start);
>
> if (!removed) cout \<\< "Not found" \<\< endl; }
>
> }

return 0; }

**1)** **Write** **a** **c++** **code** **for** **implementation**
**of** **stack** **push** **and** **pop** **operation.**

\#include \<iostream\>

using namespace std;

\#define MAX 1000

int main() {

> int stack\[MAX\]; // Array to store our stack elements
>
> int top = -1; // Top of stack, -1 means empty
>
> // Let's test pushing some elements
>
> // Push 10
>
> if (top \>= MAX - 1) {
>
> cout \<\< "Stack overflow!"; // Stack is full
>
> } else {
>
> // If not full, add element on top
>
> stack\[++top\] = 10;
>
> cout \<\< "10 pushed into stack\n";
>
> }
>
> // Push 20
>
> if (top \>= MAX - 1) {
>
> cout \<\< "Stack overflow!";
>
> } else {
>
> stack\[++top\] = 20;
>
> cout \<\< "20 pushed into stack\n";

}

// Push 30

if (top \>= MAX - 1) {

> cout \<\< "Stack overflow!";

} else {

> stack\[++top\] = 30;
>
> cout \<\< "30 pushed into stack\n";

}

// Now let's pop elements

// Pop first element

if (top \< 0) {

> cout \<\< "Stack underflow!"; // Nothing to pop

} else {

> // If not empty, remove top element
>
> int x = stack\[top--\];
>
> cout \<\< x \<\< " popped from stack\n";

}

// Pop second element

if (top \< 0) {

> cout \<\< "Stack underflow!";

} else {

> int x = stack\[top--\];
>
> cout \<\< x \<\< " popped from stack\n";

}

> return 0;

}

**2)** **Write** **a** **c++** **code** **for** **balanced**
**parentheses.**

\#include \<iostream\>

\#include \<string\>

using namespace std;

int main() {

> string expr = "{\[()\]}";
>
> // Create a simple array-based stack
>
> char stack\[100\]; // Assuming max expression length is 100
>
> int top = -1; // Initial stack position
>
> bool isBalanced = true;
>
> // Traverse the expression
>
> for (int i = 0; i \< expr.length(); i++) {
>
> // If current character is opening bracket, push to stack
>
> if (expr\[i\] == '(' \|\| expr\[i\] == '{' \|\| expr\[i\] == '\[') {
>
> top++;
>
> stack\[top\] = expr\[i\];
>
> continue;
>
> }
>
> // If stack is empty, there's no matching opening bracket
>
> if (top == -1) {
>
> isBalanced = false;
>
> break;
>
> }
>
> char check;
>
> if (expr\[i\] == ')') {
>
> // Pop from stack and check if it matches
>
> check = stack\[top\];
>
> top--;
>
> if (check != '(') {
>
> isBalanced = false;
>
> break;
>
> }
>
> }
>
> else if (expr\[i\] == '}') {
>
> check = stack\[top\];
>
> top--;
>
> if (check != '{') {
>
> isBalanced = false;
>
> break;
>
> }
>
> }
>
> else if (expr\[i\] == '\]') {
>
> check = stack\[top\];
>
> top--;
>
> if (check != '\[') {
>
> isBalanced = false;
>
> break;
>
> }
>
> }
>
> }
>
> // If stack is not empty, some opening brackets didn't get matched
>
> if (top != -1)
>
> isBalanced = false;
>
> // Print result
>
> if (isBalanced)
>
> cout \<\< "Balanced";
>
> else
>
> cout \<\< "Not Balanced";
>
> return 0;

}

**3)** **Write** **a** **c++** **code** **for** **implementing**
**queue** **using** **two** **stacks.**

\#include \<iostream\>

using namespace std;

\#define MAX 1000

int main() {

> // We'll need two stacks to implement our queue
>
> int s1\[MAX\], s2\[MAX\]; // Our two stacks
>
> int top1 = -1, top2 = -1; // Top pointers for each stack

// Let's add some items to our queue

// Enqueue operation - simply push to first stack

// Enqueue 1

s1\[++top1\] = 1;

cout \<\< "1 added to queue\n";

// Enqueue 2

s1\[++top1\] = 2;

cout \<\< "2 added to queue\n";

// Enqueue 3

s1\[++top1\] = 3;

cout \<\< "3 added to queue\n";

// Now let's remove items (dequeue)

// Dequeue first item

// If both stacks are empty, queue is empty

if (top1 == -1 && top2 == -1) {

> cout \<\< "Queue is empty!\n";

} else {

> // If s2 is empty, transfer all elements from s1
>
> if (top2 == -1) {
>
> // Move all items from s1 to s2
>
> while (top1 \>= 0) {
>
> s2\[++top2\] = s1\[top1--\];
>
> }
>
> }
>
> // Get the front item from s2
>
> int x = s2\[top2--\];
>
> cout \<\< x \<\< " removed from queue\n";

}

// Dequeue second item

if (top1 == -1 && top2 == -1) {

> cout \<\< "Queue is empty!\n";

} else {

> // If s2 is empty, transfer all elements from s1
>
> if (top2 == -1) {
>
> // Move all items from s1 to s2
>
> while (top1 \>= 0) {
>
> s2\[++top2\] = s1\[top1--\];
>
> }
>
> }
>
> // Get the front item from s2
>
> int x = s2\[top2--\];
>
> cout \<\< x \<\< " removed from queue\n";

}

// Enqueue 4

s1\[++top1\] = 4;

cout \<\< "4 added to queue\n";

> // Dequeue third item
>
> if (top1 == -1 && top2 == -1) {
>
> cout \<\< "Queue is empty!\n";
>
> } else {
>
> // If s2 is empty, transfer all elements from s1
>
> if (top2 == -1) {
>
> // Move all items from s1 to s2
>
> while (top1 \>= 0) {
>
> s2\[++top2\] = s1\[top1--\];
>
> }
>
> }
>
> // Get the front item from s2
>
> int x = s2\[top2--\];
>
> cout \<\< x \<\< " removed from queue\n";
>
> }
>
> return 0;

}

**4)** **Write** **a** **c++** **code** **for** **implementing**
**queue** **front** **and** **rear** **operation.**

\#include \<iostream\>

using namespace std;

\#define MAX 1000

int main() {

> int queue\[MAX\]; // Array to hold our queue
>
> int front = 0; // Index for the front item
>
> int rear = -1; // Index for the rear item
>
> int size = 0; // Current number of items
>
> // Let's add some items to our queue
>
> // Enqueue 10
>
> if (size == MAX) {
>
> cout \<\< "Queue is full!\n";
>
> } else {
>
> // Circular increment of rear
>
> rear = (rear + 1) % MAX;
>
> queue\[rear\] = 10;
>
> size++;
>
> cout \<\< "10 added to queue\n";
>
> }
>
> // Enqueue 20
>
> if (size == MAX) {
>
> cout \<\< "Queue is full!\n";
>
> } else {
>
> rear = (rear + 1) % MAX;
>
> queue\[rear\] = 20;
>
> size++;
>
> cout \<\< "20 added to queue\n";
>
> }

// Enqueue 30

if (size == MAX) {

> cout \<\< "Queue is full!\n";

} else {

> rear = (rear + 1) % MAX;
>
> queue\[rear\] = 30;
>
> size++;
>
> cout \<\< "30 added to queue\n";

}

// Let's check the front and rear elements

if (size == 0) {

> cout \<\< "Queue is empty!\n";

} else {

> cout \<\< "Front element: " \<\< queue\[front\] \<\< endl;
>
> cout \<\< "Rear element: " \<\< queue\[rear\] \<\< endl;

}

// Now let's remove an item

if (size == 0) {

> cout \<\< "Queue is empty!\n";

} else {

> int item = queue\[front\];
>
> // Circular increment of front
>
> front = (front + 1) % MAX;
>
> size--;
>
> cout \<\< item \<\< " removed\n";
>
> }
>
> // Check front again after removal
>
> if (size == 0) {
>
> cout \<\< "Queue is empty!\n";
>
> } else {
>
> cout \<\< "Front element after dequeue: " \<\< queue\[front\] \<\<
> endl;
>
> }
>
> return 0;

}

**5)** **Write** **a** **c++** **code** **for** **counting** **total**
**number** **of** **nodes** **in** **linked** **list.**

\#include \<iostream\>

using namespace std;

int main() {

> // Let's create a simple linked list structure
>
> struct Node {
>
> int data;
>
> Node\* next;
>
> };
>
> // Create nodes for our list
>
> Node\* head = new Node();
>
> Node\* second = new Node();
>
> Node\* third = new Node();

Node\* fourth = new Node();

// Assign data values

head-\>data = 1;

second-\>data = 2;

third-\>data = 3;

fourth-\>data = 4;

// Connect nodes to form a linked list

head-\>next = second;

second-\>next = third;

third-\>next = fourth;

fourth-\>next = NULL;

// Now let's count the nodes

int count = 0;

Node\* current = head;

// Traverse the linked list and count nodes

while (current != NULL) {

> count++;
>
> current = current-\>next;

}

// Print the result

cout \<\< "Number of nodes: " \<\< count \<\< endl;

// Clean up memory

> delete head;
>
> delete second;
>
> delete third;
>
> delete fourth;
>
> return 0;

}

**6)** **Write** **a** **c++** **code** **for** **finding** **cycle**
**in** **the** **linked** **list.**

\#include \<iostream\>

using namespace std;

int main() {

> // Let's create a simple linked list structure
>
> struct Node {
>
> int data;
>
> Node\* next;
>
> };
>
> // Create nodes for our list
>
> Node\* head = new Node();
>
> Node\* second = new Node();
>
> Node\* third = new Node();
>
> Node\* fourth = new Node();
>
> // Assign data values
>
> head-\>data = 1;

second-\>data = 2;

third-\>data = 3;

fourth-\>data = 4;

// Connect nodes to form a linked list

head-\>next = second;

second-\>next = third;

third-\>next = fourth;

fourth-\>next = NULL; // No cycle initially

// Let's check for cycle using Floyd's cycle-finding algorithm

// Also known as "tortoise and hare" algorithm

// No cycle case

Node\* slow = head;

Node\* fast = head;

bool hasCycle = false;

while (fast != NULL && fast-\>next != NULL) {

> slow = slow-\>next; // Move one step
>
> fast = fast-\>next-\>next; // Move two steps
>
> // If they meet, we found a cycle
>
> if (slow == fast) {
>
> hasCycle = true;
>
> break;
>
> }

}

// Print result for no cycle case

cout \<\< "Has cycle? " \<\< (hasCycle ? "Yes" : "No") \<\< endl;

// Now let's create a cycle and test again (4 points back to 2)

fourth-\>next = second;

// Reset our pointers

slow = head;

fast = head;

hasCycle = false;

// Check for cycle again

while (fast != NULL && fast-\>next != NULL) {

> slow = slow-\>next;
>
> fast = fast-\>next-\>next;
>
> if (slow == fast) {
>
> hasCycle = true;
>
> break;
>
> }

}

// Print result for cycle case

cout \<\< "Has cycle after modification? " \<\< (hasCycle ? "Yes" :
"No") \<\< endl;

// Note: In a real program, we would need to clean up memory differently

// since we created a cycle. Here we're skipping that to keep code
simple.

> return 0;

}

**7)** **Write** **a** **c++** **code** **for** **reversing** **linked**
**list.**

\#include \<iostream\>

using namespace std;

int main() {

> // Let's create a simple linked list structure
>
> struct Node {
>
> int data;
>
> Node\* next;
>
> };
>
> // Create nodes for our list
>
> Node\* head = new Node();
>
> Node\* second = new Node();
>
> Node\* third = new Node();
>
> Node\* fourth = new Node();
>
> // Assign data values
>
> head-\>data = 1;
>
> second-\>data = 2;
>
> third-\>data = 3;
>
> fourth-\>data = 4;

// Connect nodes to form a linked list

head-\>next = second;

second-\>next = third;

third-\>next = fourth;

fourth-\>next = NULL;

// Print original list

cout \<\< "Original list: ";

Node\* temp = head;

while (temp != NULL) {

> cout \<\< temp-\>data \<\< " ";
>
> temp = temp-\>next;

}

cout \<\< endl;

// Now let's reverse the list

Node\* prev = NULL; // Previous node

Node\* current = head; // Current node

Node\* next = NULL; // Next node

// Traverse the list

while (current != NULL) {

> // Save next node
>
> next = current-\>next;
>
> // Reverse current node's pointer
>
> current-\>next = prev;
>
> // Move pointers one position ahead
>
> prev = current;
>
> current = next;
>
> }
>
> // New head is the previous last node
>
> head = prev;
>
> // Print reversed list
>
> cout \<\< "Reversed list: ";
>
> temp = head;
>
> while (temp != NULL) {
>
> cout \<\< temp-\>data \<\< " ";
>
> temp = temp-\>next;
>
> }
>
> cout \<\< endl;
>
> // Clean up memory
>
> current = head;
>
> while (current != NULL) {
>
> next = current-\>next;
>
> delete current;
>
> current = next;
>
> }
>
> return 0;

}

**8)** **Write** **a** **c++** **code** **for** **implementing**
**bubble** **sort.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array to sort
>
> int arr\[\] = {64, 34, 25, 12, 22, 11, 90};
>
> int n = sizeof(arr)/sizeof(arr\[0\]);
>
> // Print original array
>
> cout \<\< "Original array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> // Bubble sort algorithm
>
> bool swapped;
>
> // Traverse through all array elements
>
> for (int i = 0; i \< n-1; i++) {
>
> swapped = false;
>
> // Last i elements are already in place
>
> for (int j = 0; j \< n-i-1; j++) {
>
> // If current element is greater than next element
>
> if (arr\[j\] \> arr\[j+1\]) {
>
> // Swap them
>
> int temp = arr\[j\];
>
> arr\[j\] = arr\[j+1\];
>
> arr\[j+1\] = temp;
>
> swapped = true;
>
> }
>
> }
>
> // If no swapping occurred in this pass, array is sorted
>
> if (swapped == false)
>
> break;
>
> }
>
> // Print sorted array
>
> cout \<\< "Sorted array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> return 0;

}

**9)** **Write** **a** **c++** **code** **for** **implementing**
**selection** **sort.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array to sort
>
> int arr\[\] = {64, 25, 12, 22, 11};

int n = sizeof(arr)/sizeof(arr\[0\]);

// Print original array

cout \<\< "Original array: ";

for (int i = 0; i \< n; i++)

> cout \<\< arr\[i\] \<\< " ";

cout \<\< endl;

// Selection sort algorithm

// Traverse through all array elements

for (int i = 0; i \< n-1; i++) {

> // Find the minimum element in unsorted part
>
> int min_idx = i;
>
> for (int j = i+1; j \< n; j++) {
>
> if (arr\[j\] \< arr\[min_idx\])
>
> min_idx = j;
>
> }
>
> // Swap the found minimum element with the first element
>
> if (min_idx != i) {
>
> int temp = arr\[min_idx\];
>
> arr\[min_idx\] = arr\[i\];
>
> arr\[i\] = temp;
>
> }

}

// Print sorted array

cout \<\< "Sorted array: ";

> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> return 0;

}

**10)** **Write** **a** **c++** **code** **for** **implementing**
**insertion** **sort.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array to sort
>
> int arr\[\] = {12, 11, 13, 5, 6};
>
> int n = sizeof(arr)/sizeof(arr\[0\]);
>
> // Print original array
>
> cout \<\< "Original array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> // Insertion sort algorithm
>
> // Start from the second element
>
> for (int i = 1; i \< n; i++) {
>
> // Element to be compared
>
> int key = arr\[i\];
>
> // Index of element before current
>
> int j = i - 1;
>
> // Move elements greater than key to one position ahead
>
> while (j \>= 0 && arr\[j\] \> key) {
>
> arr\[j + 1\] = arr\[j\];
>
> j = j - 1;
>
> }
>
> // Place key at its correct position
>
> arr\[j + 1\] = key;
>
> }
>
> // Print sorted array
>
> cout \<\< "Sorted array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> return 0;

}

**11)** **Write** **a** **c++** **code** **for** **implementing**
**quick** **sort.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array to sort
>
> int arr\[\] = {10, 7, 8, 9, 1, 5};
>
> int n = sizeof(arr)/sizeof(arr\[0\]);
>
> // Print original array
>
> cout \<\< "Original array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> // Using a manual stack to implement non-recursive quicksort
>
> // This simulates the recursive calls
>
> int stack\[n\];
>
> int top = -1;
>
> // Push initial values of l and h to stack
>
> stack\[++top\] = 0; // low
>
> stack\[++top\] = n - 1; // high
>
> // Keep popping from stack while it's not empty
>
> while (top \>= 0) {
>
> // Pop h and l
>
> int high = stack\[top--\];
>
> int low = stack\[top--\];
>
> // Partition the array
>
> // Select the rightmost element as pivot
>
> int pivot = arr\[high\];
>
> // Index of smaller element
>
> int i = (low - 1);
>
> // Check each element against pivot
>
> for (int j = low; j \<= high - 1; j++) {
>
> // If current element is smaller than pivot
>
> if (arr\[j\] \< pivot) {
>
> i++; // increment index of smaller element
>
> // Swap elements
>
> int temp = arr\[i\];
>
> arr\[i\] = arr\[j\];
>
> arr\[j\] = temp;
>
> }
>
> }
>
> // Swap pivot to its correct position
>
> int temp = arr\[i + 1\];
>
> arr\[i + 1\] = arr\[high\];
>
> arr\[high\] = temp;
>
> int partitionIndex = i + 1;
>
> // If there are elements on left side of pivot,
>
> // push left side to stack
>
> if (partitionIndex - 1 \> low) {
>
> stack\[++top\] = low;
>
> stack\[++top\] = partitionIndex - 1;
>
> }
>
> // If there are elements on right side of pivot,
>
> // push right side to stack
>
> if (partitionIndex + 1 \< high) {
>
> stack\[++top\] = partitionIndex + 1;
>
> stack\[++top\] = high;
>
> }
>
> }
>
> // Print sorted array
>
> cout \<\< "Sorted array: ";
>
> for (int i = 0; i \< n; i++)
>
> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> return 0;

}

**12)** **Write** **a** **c++** **code** **for** **implementing**
**merge** **sort.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array to sort
>
> int arr\[\] = {12, 11, 13, 5, 6, 7};

int n = sizeof(arr)/sizeof(arr\[0\]);

// Print original array

cout \<\< "Original array: ";

for (int i = 0; i \< n; i++)

> cout \<\< arr\[i\] \<\< " ";

cout \<\< endl;

// Merge sort is typically recursive, but we'll use an iterative
approach

// We'll sort subarrays of increasing size

int temp\[n\]; // Temporary array for merging

// Start with size=1 subarrays and double the size in each iteration

for (int size = 1; size \< n; size = 2\*size) {

> // Pick starting points of different subarrays of current size
>
> for (int leftStart = 0; leftStart \< n-1; leftStart += 2\*size) {
>
> // Find ending points of left and right subarrays
>
> int mid = min(leftStart + size - 1, n-1);
>
> int rightEnd = min(leftStart + 2\*size - 1, n-1);
>
> // Merge the subarrays
>
> int left = leftStart;
>
> int right = mid + 1;
>
> int k = leftStart;
>
> // Start index of left subarray
>
> // Start index of right subarray

// Initial index of temp array

> // Merge the two subarrays into temp array
>
> while (left \<= mid && right \<= rightEnd) {
>
> if (arr\[left\] \<= arr\[right\]) {
>
> temp\[k++\] = arr\[left++\];
>
> }
>
> else {
>
> temp\[k++\] = arr\[right++\];
>
> }
>
> }
>
> // Copy remaining elements of left subarray
>
> while (left \<= mid) {
>
> temp\[k++\] = arr\[left++\];
>
> }
>
> // Copy remaining elements of right subarray
>
> while (right \<= rightEnd) {
>
> temp\[k++\] = arr\[right++\];
>
> }
>
> // Copy back from temp to original array
>
> for (int i = leftStart; i \<= rightEnd; i++) {
>
> arr\[i\] = temp\[i\];
>
> }
>
> }

}

// Print sorted array

cout \<\< "Sorted array: ";

for (int i = 0; i \< n; i++)

> cout \<\< arr\[i\] \<\< " ";
>
> cout \<\< endl;
>
> return 0;

}

**13)** **Write** **a** **c++** **code** **for** **implementing**
**linear** **search.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize an array and value to search
>
> int arr\[\] = {2, 3, 4, 10, 40};
>
> int n = sizeof(arr)/sizeof(arr\[0\]);
>
> int x = 10; // Value to search
>
> // Linear search algorithm
>
> int result = -1; // Initialize as not found
>
> // Check each element one by one
>
> for (int i = 0; i \< n; i++) {
>
> if (arr\[i\] == x) {
>
> result = i; // Save index if found
>
> break; // Exit loop
>
> }
>
> }
>
> // Print result
>
> if (result == -1)
>
> cout \<\< "Element not found";
>
> else
>
> cout \<\< "Element found at index " \<\< result;
>
> return 0;

}

**14)** **Write** **a** **c++** **code** **for** **implementing**
**binary** **search.**

\#include \<iostream\>

using namespace std;

int main() {

> // Initialize a sorted array and value to search
>
> int arr\[\] = {2, 3, 4, 10, 40};
>
> int n = sizeof(arr)/sizeof(arr\[0\]);
>
> int x = 10; // Value to search
>
> // Binary search algorithm
>
> int result = -1; // Initialize as not found
>
> int left = 0; // Left boundary
>
> int right = n-1; // Right boundary
>
> while (left \<= right) {
>
> // Find middle element
>
> int mid = left + (right - left) / 2;
>
> // Check if x is at mid
>
> if (arr\[mid\] == x) {
>
> result = mid;
>
> break;
>
> }
>
> // If x is greater, ignore left half
>
> if (arr\[mid\] \< x)
>
> left = mid + 1;
>
> // If x is smaller, ignore right half
>
> else
>
> right = mid - 1;
>
> }
>
> // Print result
>
> if (result == -1)
>
> cout \<\< "Element not found";
>
> else
>
> cout \<\< "Element found at index " \<\< result;
>
> return 0;

}

**15)** **Write** **a** **c++** **code** **for** **finding** **height**
**of** **the** **BST.**

\#include \<iostream\>

using namespace std;

int main() {

> // Define a binary tree node
>
> struct Node {
>
> int data;
>
> Node\* left;
>
> Node\* right;
>
> };
>
> // Create a function to make a new node
>
> auto newNode = \[\](int data) -\> Node\* {
>
> Node\* node = new Node();
>
> node-\>data = data;
>
> node-\>left = NULL;
>
> node-\>right = NULL;
>
> return node;
>
> };
>
> // Create a sample BST
>
> Node\* root = newNode(50);
>
> root-\>left = newNode(30);
>
> root-\>right = newNode(70);
>
> root-\>left-\>left = newNode(20);
>
> root-\>left-\>right = newNode(40);
>
> root-\>right-\>left = newNode(60);
>
> root-\>right-\>right = newNode(80);
>
> // This is a special case where we need some recursion-like behavior

// We'll use a manual stack to simulate the recursion for finding height

// We need to keep track of nodes along with their levels

struct NodeWithHeight {

> Node\* node;
>
> int height;

};

NodeWithHeight stack\[100\]; // Assuming stack size of 100 is enough

int top = -1;

// Push root with height 1

stack\[++top\] = {root, 1};

int maxHeight = 0;

// Process until stack is empty

while (top \>= 0) {

> // Pop top node and its height
>
> NodeWithHeight current = stack\[top--\];
>
> // Update max height if current height is greater
>
> if (current.height \> maxHeight)
>
> maxHeight = current.height;
>
> // Push children to stack with height+1
>
> if (current.node-\>right)
>
> stack\[++top\] = {current.node-\>right, current.height + 1};
>
> if (current.node-\>left)
>
> stack\[++top\] = {current.node-\>left, current.height + 1};
>
> }
>
> cout \<\< "Height of BST: " \<\< maxHeight \<\< endl;
>
> // Clean up memory
>
> // Would ideally use another stack traversal to free all nodes
>
> return 0;

}

**16)** **Write** **a** **c++** **code** **for** **counting** **total**
**number** **of** **nodes** **in** **BST.**

\#include \<iostream\>

using namespace std;

int main() {

> // Define a binary tree node
>
> struct Node {
>
> int data;
>
> Node\* left;
>
> Node\* right;
>
> };
>
> // Create a function to make a new node
>
> auto newNode = \[\](int data) -\> Node\* {
>
> Node\* node = new Node();
>
> node-\>data = data;
>
> node-\>left = NULL;
>
> node-\>right = NULL;
>
> return node;

};

// Create a sample BST

Node\* root = newNode(50);

root-\>left = newNode(30);

root-\>right = newNode(70);

root-\>left-\>left = newNode(20);

root-\>left-\>right = newNode(40);

root-\>right-\>left = newNode(60);

root-\>right-\>right = newNode(80);

// Use a stack to count nodes (simulating recursion)

Node\* stack\[100\]; // Assuming stack size of 100 is enough

int top = -1;

if (root != NULL)

> stack\[++top\] = root;

int count = 0;

// Process until stack is empty

while (top \>= 0) {

> // Pop top node
>
> Node\* current = stack\[top--\];
>
> // Increment count
>
> count++;
>
> // Push children to stack
>
> if (current-\>right)
>
> stack\[++top\] = current-\>right;
>
> if (current-\>left)
>
> stack\[++top\] = current-\>left;
>
> }
>
> cout \<\< "Total number of nodes in BST: " \<\< count \<\< endl;
>
> // Clean up memory
>
> // Would ideally use another stack traversal to free all nodes
>
> return 0;

}

**17)** **Write** **a** **c++** **code** **for** **implementing**
**BFS.**

\#include \<iostream\>

\#include \<list\>

\#include \<queue\>

using namespace std;

int main() {

> // Define number of vertices
>
> int V = 4;

// Create adjacency lists

list\<int\> \*adj = new list\<int\>\[V\];

// Add edges manually (equivalent to addEdge function)

adj\[0\].push_back(1);

adj\[0\].push_back(2);

adj\[1\].push_back(2);

adj\[2\].push_back(0);

adj\[2\].push_back(3);

adj\[3\].push_back(3);

// Define source vertex for BFS

int s = 2;

cout \<\< "BFS starting from vertex 2: ";

// BFS implementation

// Mark all vertices as not visited

bool \*visited = new bool\[V\];

for (int i = 0; i \< V; i++)

> visited\[i\] = false;

// Create a queue for BFS

queue\<int\> q;

// Mark the current node as visited and enqueue it

visited\[s\] = true;

> q.push(s);
>
> // Variable to store dequeued vertex
>
> int current;
>
> // BFS traversal loop
>
> while (!q.empty()) {
>
> // Dequeue a vertex from queue and print it
>
> current = q.front();
>
> cout \<\< current \<\< " ";
>
> q.pop();
>
> // Get all adjacent vertices of the dequeued vertex
>
> // If an adjacent hasn't been visited, mark it visited and enqueue it
>
> for (list\<int\>::iterator i = adj\[current\].begin(); i !=
> adj\[current\].end(); ++i) {
>
> if (!visited\[\*i\]) {
>
> visited\[\*i\] = true;
>
> q.push(\*i);
>
> }
>
> }
>
> }
>
> // Clean up memory
>
> delete\[\] visited;
>
> delete\[\] adj;
>
> return 0;

}

**18)** **Write** **a** **c++** **code** **for** **implementing**
**DFS.**

\#include \<iostream\>

\#include \<list\>

using namespace std;

// Graph class

class Graph {

> int V; // Number of vertices
>
> list\<int\> \*adj; // Adjacency list
>
> // DFS helper function
>
> void DFSUtil(int v, bool visited\[\]) {
>
> // Mark the current node as visited and print it
>
> visited\[v\] = true;
>
> cout \<\< v \<\< " ";
>
> // Recur for all the vertices adjacent to this vertex
>
> list\<int\>::iterator i;
>
> for (i = adj\[v\].begin(); i != adj\[v\].end(); ++i)
>
> if (!visited\[\*i\])
>
> DFSUtil(\*i, visited);
>
> }

public:

> // Constructor
>
> Graph(int V) {
>
> this-\>V = V;
>
> adj = new list\<int\>\[V\];
>
> }
>
> // Add an edge to the graph
>
> void addEdge(int v, int w) {
>
> adj\[v\].push_back(w); // Add w to v's list
>
> }
>
> // DFS traversal from a given vertex v
>
> void DFS(int v) {
>
> // Mark all the vertices as not visited
>
> bool \*visited = new bool\[V\];
>
> for (int i = 0; i \< V; i++)
>
> visited\[i\] = false;
>
> // Call the recursive helper function
>
> DFSUtil(v, visited);
>
> }

};

// Main function to test DFS

int main() {

> // Create a graph
>
> Graph g(4);
>
> g.addEdge(0, 1);
>
> g.addEdge(0, 2);
>
> g.addEdge(1, 2);
>
> g.addEdge(2, 0);
>
> g.addEdge(2, 3);
>
> g.addEdge(3, 3);
>
> cout \<\< "DFS starting from vertex 2: ";
>
> g.DFS(2);
>
> return 0;

}

**19)** **Write** **a** **c++** **code** **for** **implementing**
**graph** **adjacency** **list** **and** **adjacency** **matrix.**

\#include \<iostream\>

\#include \<vector\>

using namespace std;

// Graph class with both adjacency list and matrix

class Graph {

> int V; // Number of vertices
>
> // Adjacency list
>
> vector\<vector\<int\>\> adjList;
>
> // Adjacency matrix
>
> vector\<vector\<int\>\> adjMatrix;

public:

// Constructor

Graph(int V) {

> this-\>V = V;
>
> // Initialize adjacency list
>
> adjList.resize(V);
>
> // Initialize adjacency matrix with zeros
>
> adjMatrix.resize(V, vector\<int\>(V, 0));

}

// Add an edge to the graph

void addEdge(int u, int v) {

> // Update adjacency list
>
> adjList\[u\].push_back(v);
>
> // Update adjacency matrix
>
> adjMatrix\[u\]\[v\] = 1;

}

// Print adjacency list

void printAdjList() {

> cout \<\< "Adjacency List:" \<\< endl;
>
> for (int i = 0; i \< V; i++) {
>
> cout \<\< i \<\< " -\> ";
>
> for (auto j: adjList\[i\])
>
> cout \<\< j \<\< " ";
>
> cout \<\< endl;
>
> }
>
> }
>
> // Print adjacency matrix
>
> void printAdjMatrix() {
>
> cout \<\< "Adjacency Matrix:" \<\< endl;
>
> for (int i = 0; i \< V; i++) {
>
> for (int j = 0; j \< V; j++)
>
> cout \<\< adjMatrix\[i\]\[j\] \<\< " ";
>
> cout \<\< endl;
>
> }
>
> }

};

// Main function to test graph representations

int main() {

> // Create a graph with 5 vertices
>
> Graph g(5);
>
> // Add edges
>
> g.addEdge(0, 1);
>
> g.addEdge(0, 4);
>
> g.addEdge(1, 2);
>
> g.addEdge(1, 3);
>
> g.addEdge(1, 4);
>
> g.addEdge(2, 3);
>
> g.addEdge(3, 4);
>
> // Print adjacency list and matrix
>
> g.printAdjList();
>
> cout \<\< endl;
>
> g.printAdjMatrix();
>
> return 0;

}

> **20)** **Write** **a** **c++** **code** **to** **implement** **hash**
> **table.**

\#include \<iostream\>

\#include \<list\>

\#include \<string\>

using namespace std;

// Hash table class using chaining for collision handling

class HashTable {

> // Size of hash table
>
> int capacity;
>
> // Pointer to an array of linked lists
>
> list\<pair\<string, int\>\> \*table;

public:

> // Constructor
>
> HashTable(int capacity) {
>
> this-\>capacity = capacity;
>
> table = new list\<pair\<string, int\>\>\[capacity\];

}

// Hash function to map keys to table index

int hashFunction(string key) {

> int hash = 0;
>
> // Simple hash: sum ASCII values of characters
>
> for (char c : key)
>
> hash += c;
>
> return hash % capacity;

}

// Insert a key-value pair into hash table

void insert(string key, int value) {

> // Get index from hash function
>
> int index = hashFunction(key);
>
> // Check if key already exists
>
> auto &cell = table\[index\];
>
> auto it = begin(cell);
>
> bool keyExists = false;
>
> while (it != end(cell)) {
>
> if (it-\>first == key) {
>
> // If key exists, update value
>
> keyExists = true;
>
> it-\>second = value;
>
> cout \<\< "Updated key: " \<\< key \<\< endl;
>
> break;
>
> }
>
> it++;
>
> }
>
> // If key doesn't exist, insert at the end
>
> if (!keyExists) {
>
> cell.emplace_back(key, value);
>
> cout \<\< "Inserted key: " \<\< key \<\< endl;
>
> }

}

// Remove a key from hash table

void remove(string key) {

> // Get index from hash function
>
> int index = hashFunction(key);
>
> // Check if key exists
>
> auto &cell = table\[index\];
>
> auto it = begin(cell);
>
> bool keyExists = false;
>
> while (it != end(cell)) {
>
> if (it-\>first == key) {
>
> // If key exists, remove it
>
> keyExists = true;
>
> it = cell.erase(it);
>
> cout \<\< "Removed key: " \<\< key \<\< endl;
>
> break;
>
> }
>
> it++;
>
> }
>
> // If key doesn't exist
>
> if (!keyExists) {
>
> cout \<\< "Key not found: " \<\< key \<\< endl;
>
> }

}

// Search for a key in hash table

int get(string key) {

> // Get index from hash function
>
> int index = hashFunction(key);
>
> // Check if key exists
>
> auto &cell = table\[index\];
>
> auto it = begin(cell);
>
> while (it != end(cell)) {
>
> if (it-\>first == key) {
>
> // If key exists, return value
>
> return it-\>second;
>
> }
>
> it++;
>
> }
>
> // If key doesn't exist
>
> cout \<\< "Key not found: " \<\< key \<\< endl;
>
> return -1;
>
> }
>
> // Display the hash table
>
> void display() {
>
> for (int i = 0; i \< capacity; i++) {
>
> cout \<\< "Index " \<\< i \<\< ": ";
>
> for (auto it = table\[i\].begin(); it != table\[i\].end(); it++) {
>
> cout \<\< "(" \<\< it-\>first \<\< ", " \<\< it-\>second \<\< ") ";
>
> }
>
> cout \<\< endl;
>
> }
>
> }

};

// Main function to test hash table

int main() {

> // Create a hash table with capacity 10
>
> HashTable ht(10);
>
> // Insert some key-value pairs
>
> ht.insert("apple", 5);
>
> ht.insert("banana", 10);
>
> ht.insert("orange", 15);
>
> ht.insert("grape", 20);
>
> // Display the hash table
>
> cout \<\< "\nHash Table:" \<\< endl;
>
> ht.display();
>
> // Search for keys
>
> cout \<\< "\nValue for key 'apple': " \<\< ht.get("apple") \<\< endl;
>
> cout \<\< "Value for key 'orange': " \<\< ht.get("orange") \<\< endl;
>
> cout \<\< "Value for key 'mango': " \<\< ht.get("mango") \<\< endl;
>
> // Update a key
>
> ht.insert("apple", 25);
>
> // Remove a key
>
> ht.remove("banana");
>
> // Display the updated hash table
>
> cout \<\< "\nUpdated Hash Table:" \<\< endl;
>
> ht.display();
>
> return 0;

}



## 1. Stack

**Theory:**
A stack is a linear data structure that follows the Last In First Out (LIFO) principle. This means the last element added to the stack will be the first one to be removed. Think of it like a stack of plates—you can only take the top plate off, and you can only add new plates to the top.

**Key Operations:**
- **Push:** Add an element to the top of the stack  
- **Pop:** Remove the top element from the stack  
- **Peek/Top:** View the top element without removing it

**Time Complexity:**
- Push: O(1)  
- Pop: O(1)  
- Peek: O(1)

**Applications:**
- Function call management (call stack)  
- Expression evaluation and syntax parsing  
- Undo mechanisms in text editors  
- Backtracking algorithms

---

## 2. Balanced Parentheses

**Theory:**
Use a stack to verify if an expression has properly balanced parentheses/brackets. For every opening bracket, there should be a corresponding closing bracket in the correct order.

**Algorithm:**
1. Create an empty stack.  
2. Scan the expression from left to right.  
3. If you encounter an opening bracket `(`, `[`, or `{`, push it onto the stack.  
4. If you encounter a closing bracket `)`, `]`, or `}`, then:
   - If the stack is empty → the expression is unbalanced.  
   - Otherwise, pop the stack and check if it matches the closing bracket. If not → unbalanced.  
5. After scanning, if the stack is empty → the expression is balanced; otherwise, it’s unbalanced.

**Applications:**
- Compiler syntax checking  
- Text editors with bracket matching  
- Mathematical expression validation

---

## 3. Queue Using Two Stacks

**Theory:**
A queue follows First In First Out (FIFO), opposite of a stack. By using two stacks, we can simulate queue behavior: one stack for enqueueing, the other for dequeueing.

**Algorithm:**
- **Enqueue(x):** Push `x` onto `stack1`.  
- **Dequeue():**  
  1. If `stack2` is empty, pop all elements from `stack1` and push them onto `stack2`.  
  2. Pop and return the top element from `stack2`.

**Time Complexity:**
- Enqueue: O(1)  
- Dequeue: Amortized O(1), worst case O(n)

**Applications:**
- When only stacks are available but a queue is needed  
- Data structure implementation exercises  
- Common interview problem

---

## 4. Queue Front and Rear Operations

**Theory:**
Implement a FIFO queue using a circular array to achieve O(1) time for all operations.

**Key Operations:**
- **Enqueue:** Add an element at the rear.  
- **Dequeue:** Remove an element from the front.  
- **Front:** View the front element without removing.  
- **Rear:** View the rear element without removing.

**Time Complexity:**
- All operations: O(1)

**Applications:**
- Task scheduling  
- Print job management  
- BFS algorithm implementation

---

## 5. Linked List Node Counting

**Theory:**
A linked list consists of nodes where each node has a value and a pointer to the next node. Nodes need not be stored contiguously in memory.

**Algorithm:**
1. Initialize `count = 0`.  
2. Set `current = head`.  
3. While `current != NULL`:  
   - `count++`  
   - `current = current->next`  
4. Return `count`.

**Time Complexity:**
- O(n)

**Applications:**
- Dynamic memory structures  
- Basis for other data structures (stacks, queues)  
- Frequent insert/delete operations

---

## 6. Cycle Detection in Linked List

**Theory:**
Use Floyd’s Tortoise and Hare algorithm to detect loops where a node’s `next` pointer revisits an earlier node.

**Algorithm (Floyd’s):**
1. Initialize two pointers, `slow = head`, `fast = head`.  
2. While `fast` and `fast->next` are not NULL:  
   - `slow = slow->next`  
   - `fast = fast->next->next`  
   - If `slow == fast`: cycle detected.  
3. If the loop exits: no cycle.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

**Applications:**
- Detect infinite loops  
- Validate list integrity  
- Memory leak detection

---

## 7. Reversing a Linked List

**Theory:**
Reverse the list by redirecting each node’s `next` pointer to its predecessor.

**Algorithm:**
1. `prev = NULL`, `current = head`.  
2. While `current != NULL`:  
   - `next = current->next`  
   - `current->next = prev`  
   - `prev = current`  
   - `current = next`  
3. `head = prev`.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

**Applications:**
- Reverse-order processing  
- Implementing undo operations  
- Various list-based algorithms

---

## 8. Bubble Sort

**Theory:**
Repeatedly step through the array, compare adjacent elements, and swap if out of order. Each pass “bubbles” the largest unsorted element to its correct position.

**Algorithm:**
1. For `i` from 0 to `n-2`:  
   - For `j` from 0 to `n-2-i`:  
     - If `A[j] > A[j+1]`, swap them.  
2. Optionally, if no swaps occur in a pass, the array is sorted early.

**Time Complexity:**  
- Best: O(n)  
- Average/Worst: O(n²)

**Applications:**
- Teaching basic sorting  
- Very small datasets  
- Simplicity over performance

---

## 9. Selection Sort

**Theory:**
Divide the array into sorted and unsorted parts. Repeatedly select the smallest element from the unsorted part and move it to the sorted part’s end.

**Algorithm:**
1. For `i` from 0 to `n-2`:  
   - Find `minIndex` in `A[i…n-1]`.  
   - Swap `A[i]` and `A[minIndex]`.

**Time Complexity:** O(n²)

**Applications:**
- Small arrays  
- When writes are costly  
- Educational contexts

---

## 10. Insertion Sort

**Theory:**
Build a sorted array one element at a time by inserting each new element into its correct position among previously sorted elements.

**Algorithm:**
1. For `i` from 1 to `n-1`:  
   - `key = A[i]`, `j = i-1`.  
   - While `j >= 0` and `A[j] > key`:  
     - `A[j+1] = A[j]`, `j--`.  
   - `A[j+1] = key`.

**Time Complexity:**  
- Best: O(n)  
- Average/Worst: O(n²)

**Applications:**
- Nearly sorted data  
- Online sorting  
- Subroutine in advanced sorts

---

## 11. Quick Sort

**Theory:**
Choose a pivot, partition the array into elements less than and greater than the pivot, then recursively sort both partitions.

**Algorithm:**
1. Select a pivot (commonly the last element).  
2. Partition: place elements < pivot to its left, > pivot to its right.  
3. Recursively apply to left and right subarrays.

**Time Complexity:**  
- Average/Best: O(n log n)  
- Worst: O(n²)

**Applications:**  
- General in-memory sorting  
- When average performance matters

---

## 12. Merge Sort

**Theory:**
Recursively split the array in half, sort each half, then merge them back together in sorted order.

**Algorithm:**
1. If array size ≤ 1, it’s sorted.  
2. Split into left and right halves.  
3. Recursively sort each half.  
4. Merge the two sorted halves.

**Time Complexity:** O(n log n)

**Applications:**  
- External sorting  
- Stable sort requirements  
- Linked list sorting

---

## 13. Linear Search

**Theory:**
Check each element in sequence until finding the target or reaching the end.

**Algorithm:**
1. For `i` from 0 to `n-1`:  
   - If `A[i] == target`, return `i`.  
2. Return -1 if not found.

**Time Complexity:**  
- Best: O(1)  
- Average: O(n/2)  
- Worst: O(n)

**Applications:**  
- Small or unsorted datasets  
- One-time lookups

---

## 14. Binary Search

**Theory:**
Efficiently search a sorted array by repeatedly dividing the search interval in half.

**Algorithm:**
1. `low = 0`, `high = n-1`.  
2. While `low ≤ high`:  
   - `mid = (low + high) // 2`.  
   - If `A[mid] == target`, return `mid`.  
   - Else if `A[mid] < target`, `low = mid + 1`.  
   - Else `high = mid - 1`.  
3. Return -1 if not found.

**Time Complexity:** O(log n)

**Applications:**  
- Search in sorted datasets  
- Database indexing

---

## 15. Height of Binary Search Tree (BST)

**Theory:**  
The height is the length of the longest path from the root node down to a leaf node.

**Algorithm:**  
```cpp
int height(Node* node) {
    if (!node) return 0;
    int lh = height(node->left);
    int rh = height(node->right);
    return 1 + max(lh, rh);
}
```

**Time Complexity:** O(n) worst case, O(log n) if balanced

**Applications:**  
- Tree balance analysis  
- Performance prediction

---

## 16. Counting Nodes in BST

**Theory:**  
Traverse all nodes and count each one.

**Algorithm:**  
```cpp
int countNodes(Node* node) {
    if (!node) return 0;
    return 1 + countNodes(node->left) + countNodes(node->right);
}
```

**Time Complexity:** O(n)

**Applications:**  
- Size estimation  
- Balance metrics

---

## 17. Breadth-First Search (BFS)

**Theory:**  
Level-order graph traversal using a queue, exploring neighbors before moving deeper.

**Algorithm:**  
```cpp
void BFS(int src) {
    vector<bool> visited(V, false);
    queue<int> q;
    visited[src] = true;
    q.push(src);
    while (!q.empty()) {
        int u = q.front(); q.pop();
        // process u
        for (int v : adj[u]) {
            if (!visited[v]) {
                visited[v] = true;
                q.push(v);
            }
        }
    }
}
```

**Time Complexity:** O(V + E)

**Applications:**  
- Shortest path in unweighted graphs  
- Connected components  
- Web crawlers

---

## 18. Depth-First Search (DFS)

**Theory:**  
Traverse as far along each branch before backtracking, using recursion or an explicit stack.

**Algorithm (Recursive):**  
```cpp
void DFS(int u, vector<bool>& visited) {
    visited[u] = true;
    // process u
    for (int v : adj[u]) {
        if (!visited[v]) DFS(v, visited);
    }
}
```

**Time Complexity:** O(V + E)

**Applications:**  
- Topological sorting  
- Cycle detection  
- Puzzle/maze solving

---

## 19. Graph Representation

### Adjacency List
- Store neighbors list for each vertex.  
- Space: O(V + E).  
- Edge check: O(degree).

### Adjacency Matrix
- V×V matrix, entry `[i][j] = 1` if edge exists.  
- Space: O(V²).  
- Edge check: O(1).

**Applications:**  
- Sparse vs. dense graphs  
- Network routing  
- Social networks

---

## 20. Hash Table

**Theory:**  
Associative array using a hash function to map keys to buckets.

**Components:**  
- Hash function: key → index.  
- Collision handling:  
  - Chaining (linked lists).  
  - Open addressing (probing).

**Time Complexity:**  
- Average: O(1) for insert/search/delete.  
- Worst: O(n) with high collisions.

**Applications:**  
- Database indexing  
- Caches  
- Symbol tables  
- Frequency counting
