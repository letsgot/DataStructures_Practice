
class Solution
{
    //Function to find number of strongly connected components in the graph.
    public int kosaraju(int V, ArrayList<ArrayList<Integer>> adj)
    {
        //code here
        
        // to Fill the stack
        Stack<Integer> st = new Stack<>();
        boolean vis[] = new boolean[V];
        for(int i=0;i<V;i++){
            if(vis[i]==false){
                dfs1(i,adj,vis,st);
            }
        }
        
        
        // transpose the graph 
        ArrayList<ArrayList<Integer>> trans = new ArrayList<>();
        for(int i=0;i<V;i++){
           trans.add(new ArrayList<>());
        }
        
        for(int i=0;i<V;i++){
            for(int nbr : adj.get(i)){
                trans.get(nbr).add(i);
            }
        }
        
        // get the popped from stack and get number of scc
        vis = new boolean[V];
        int count = 0;
        while(st.size()>0){
            int v = st.pop();
            if(vis[v]==false){
                dfs2(v,trans,vis);
                count++;
            }
        }
        
        return count;
    }
    
    public void dfs2(int src,ArrayList<ArrayList<Integer>> trans,boolean vis[]){
        vis[src] = true;
        
        for(int nbr : trans.get(src)){
            if(vis[nbr]==false){
                dfs2(nbr,trans,vis);
            }
        }
    }
    
    public void dfs1(int src,ArrayList<ArrayList<Integer>> adj,boolean vis[],Stack<Integer> st){
        vis[src] = true;
        
        for(int nbr : adj.get(src)){
            if(vis[nbr]==false){
                dfs1(nbr,adj,vis,st);
            }
        }
        
        st.push(src);
    }
}