### Trie（发音类似 "try"）或者说 前缀树 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。
### 请你实现 Trie 类：
- Trie() 初始化前缀树对象。
- void insert(String word) 向前缀树中插入字符串 word 。
- boolean search(String word) 如果字符串 word 在前缀树中，返回 true（即，在检索之前已经插入）；否则，返回 false 。
- boolean startsWith(String prefix) 如果之前已经插入的字符串 word 的前缀之一为 prefix ，返回 true ；否则，返回 false 。
```
class Trie {
    private Trie[]children;
    private boolean flag;//
    public Trie() {
        this.children=new Trie[26];
        this.flag=false;
    }
    
    public void insert(String word) {
        Trie node=this;// 实际上并没有创建一个新的 Trie 对象，只是创建了一个引用。
        for(int i=0;i<word.length();i++){
            char temp=word.charAt(i);
            int index=temp-'a';
            if(node.children[index]==null){
                node.children[index]=new Trie();

            }
            node=node.children[index];
        }
        node.flag=true;
    }
    
    public boolean search(String word) {
        Trie node=check(word);
        return node!=null&&node.flag;
    }
    
    public boolean startsWith(String prefix) {
        return check(prefix)!=null;
    }
    public Trie check(String word){
        Trie node=this;//头结点
        for(int i=0;i<word.length();i++){
            char temp=word.charAt(i);
            int index=temp-'a';
            if(node.children[index]==null){//检查是否存在，不用检查是否相等
                return null;
            }
            node=node.children[index];
        }
        return node;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
