//从左往右，从上往下，从右往左，从下往上的顺序<br>
//每次for结束要判断是否结束<br>
//2019.12.23<br>
```java
        int left = 0,top = 0,right=n-1,bottom = m-1;
        while(result.size()!=totalNumber){
            for(i = left;i<=right;++i){
                result.add(matrix[top][i]);
            }
            ++top;
            
            if(Finish(result,totalNumber)){
                break;
            }
            
            for(i = top;i<=bottom;++i){
                result.add(matrix[i][right]);
            }
            --right;
            if(Finish(result,totalNumber)){
                break;
            }
            
            for(i = right;i>=left;--i){
                result.add(matrix[bottom][i]);
            }
            --bottom;
            if(Finish(result,totalNumber)){
                break;
            }
            
            
            for(i = bottom;i>=top;--i){
                result.add(matrix[i][left]);
            }
            ++left;
            if(Finish(result,totalNumber)){
                break;
            }
```
