# Maximum Depth of Binary Tree
## 25th June 2026
## Recursion
```js
if(root==NULL) return 0;
return 1 + max(maxDepth(root->left),maxDepth(root->right));
```

## Same Tree

```js
if(p==NULL && q==NULL){
    return true;
}
if(p==NULL || q==NULL){
    return true;
}
if(p->val!=q->val){
    return false;
}
return sameTree(p->left,q->left) && sameTree(p->right,q->right);
```

## Invert Tree

```js
if(root==NULL)return NULL;
swap(root->left, root->right);
invertTree(root->left);
invertTree(root->right);
return root;
```

## Symmetric Tree

```js
    if(root==NULL)return false;
    return checkSymmetry(root->left,root->right);// Check for left value, right value and again recurse it with same function
```

## Preorder and Inorder

```js
buildTree(){
    if(preStart>preEnd || inStart>inEnd){
        return false;
    }
TreeNode* root=new TreeNode(ump[inorder[preStart]]);
int index=inorder[preStart];
int ljump=index-inStart;
root->left=buildTree()//preorder: preStart+1,preStart+ljump, 
//inorder: inStart, index-1
root->right=buildTree()
// preorder: prestart+newpos+1,preEnd
// index+1,inEnd
}
// Prepare an unordered_map
unordered_map<int,int> ump;
//Iterate inorder and initialize map
ump[inorder[i]]=i;

TreeNode* root=buildTree(0,preEnd-1,0,inEnd-1,preorder,inorder,ump);
return root;

```

# 9th July 2026

## Inorder and PostOrder Traversal

```js
unordered_map<int,int> ump
// Store the values from inorder vector -> ump[inorder[i]]=i;
// Build a recursive function
buildFromInAndPost();
root->left=buildFromInAndPost();
root->right=buildFromInAndPost();
return root;
```

## Design a Trie Data Structure

```js
class TrieNode{
    public:
        bool isWord;
        TrieNode* node[26];
        TrieNode(){
            for(auto &x:node){
                x->node=nullptr;
            }
            isWord=false;
        }
};
class Trie{
    public:
        TrieNode* root;
        Trie(){
            root=new TrieNode();
        }
        void insert(){
            TrieNode *p=root;
            // iterate through the word by using for loop
            // ch:word; ch-'a'; if(!p->node[ch-'a'])p->node=new TrieNode();
            // p=p->node[ch-'a'];
            // After for loop is iterated, do p->isWord;

        }
        void search(){
            // Include a flag in the search function
            // Self-explanatory for loop
        }
        void prefixSearch(){
            // Use search function and toggle the flag
        }
};
```

## Design Add and Search Words Data Structure

```js
class TrieNode{
    public:
        bool isWord;
        TrieNode* node[26];
    TrieNode(){
        for(auto &x:node){
            x=nullptr;
        }
        isWord=false;
    }
};

void addWord(){
    // Same as previous one-> iterate the word search 
    // if(!p->node[x])p->node[x]=new TrieNode();
    // p=p->node[x];
    // p->isWord=true;

}
void searchDown(string word, TrieNode* root);
void search(){
    // As usual for alphabets and iterating through p=p->node[x];
    // 
    // When you find .
    // run a recursive function searchDown(p->node[j],word.substr[i+1])
    
}
```