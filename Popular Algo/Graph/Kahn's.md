<!-- used for topological sort or cycle detection in directed graph -->



class Solution
{
    //Function to return list containing vertices in Topological order. 
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) 
    {
        // add your code here
        int in[] = new int[V];
        for(ArrayList<Integer> list : adj){
            for(int nbr : list){
                in[nbr]++;
            }
        }
        
        Queue<Integer> que = new ArrayDeque<>();
        for(int i=0;i<in.length;i++){
            if(in[i]==0){
                que.add(i);
            }
        }
        
        int ans[] = new int[V];
        int idx = 0;
        boolean vis[] = new boolean[V];
        while(que.size()>0){
            int rem = que.remove();
            
            if(vis[rem]==true){
                continue;
            }
            vis[rem] = true;
            
            ans[idx] = rem;
            idx++;
            
            for(int nbr : adj.get(rem)){
                in[nbr]--;
                if(in[nbr]==0){
                    que.add(nbr);
                }
            }
        }
        
        <!-- cycle detection check -->

        if(idx==V){
            return ans;
        }
        else{
            return new int[0];
        }
        
    }
}
