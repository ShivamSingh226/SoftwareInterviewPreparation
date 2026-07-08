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