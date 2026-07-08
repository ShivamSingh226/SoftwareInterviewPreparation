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