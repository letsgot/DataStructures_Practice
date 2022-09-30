


class Solution
{
    //Function to find a Mother Vertex in the Graph.
    public int findMotherVertex(int V, ArrayList<ArrayList<Integer>>adj)
    {
        // Code here
        Stack<Integer> st = new Stack<>();
        boolean vis[] = new boolean[V];
        
        for(int i=0;i<V;i++){
            if(vis[i]==false){
                dfs(i,adj,vis,st);
            }
        }
        
        int top = st.peek();
        
        vis = new boolean[V];
        int count = count(top,adj,vis);
        if(count==V){
            return top;
        }
        else{
            return -1;
        }
    }
    
    public void dfs(int src , ArrayList<ArrayList<Integer>>adj, boolean[]vis,Stack<Integer> st){
        vis[src] = true;
        
        for(int nbr : adj.get(src)){
            if(vis[nbr]==false)
            dfs(nbr,adj,vis,st);
        }
        
        st.push(src);
    }
    
    
    public int count(int src , ArrayList<ArrayList<Integer>>adj, boolean[]vis){
        vis[src] = true;
        
        int ans = 0;
        for(int nbr : adj.get(src)){
            if(vis[nbr]==false)
            ans += count(nbr,adj,vis);
        }
        
        return ans+1;
    }

}