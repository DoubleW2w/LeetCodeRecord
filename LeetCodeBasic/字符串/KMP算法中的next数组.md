KMP算法中的next数组

- 不减一模板

​	比如 s= "asdfasdfasdf"  得到的next[] = [0, 0, 0, 0, 1, 2, 3, 4, 5, 6, 7, 8]

```java
public int[] getNums(String s){
	int len = s.length();
    int[] next = new int[len];
    next[0] = 0;
    for (int i = 1, j = 0; i < len; i++) {
        while(j > 0 && s.charAt(i) != s.charAt(j)){  //j>0   j
            j = next[j - 1];  //next[j-1]
        }
        if(s.charAt(i) == s.charAt(j)){
            j++;
        }
        next[i] = j;
	}
    return next;
}

```

- 减一模板

​	比如 s= "asdfasdfasdf"  得到的next[] = [-1, -1, -1, -1, 0, 1, 2, 3, 4, 5, 6, 7]

```java
public int[] getNums(String s){    
    //初始化
    int j = -1;
    int[] next = new int[len];
    next[0] = j;
    for (int i = 1; i < len; i++) { 
        while(j >= 0 && s.charAt(i) != s.charAt(j+1)){  // j >= 0, j+1
            j = next[j];  //next[j]
        }
        if(s.charAt(i) == s.charAt(j+1)){  //j+1
            j++;
        }
        next[i] = j;
    }
}
```

- 哨兵，避免初始化 j=-1

```java
public int[] getNums(String s){    
    int len = s.length();
    // 原串加个空格(哨兵)，使下标从1开始，这样j从0开始，也不用初始化了
    s = " "+s;
    char[] chars = s.toCharArray();
    int[] next =new int[len + 1];
    // 构造 next 数组过程，j从0开始(空格)，i从2开始
    for(int i = 2, j = 0;i <= len;i++){
        while (j > 0 && chars[i] != chars[j + 1]) {
            j = next[j];
        }
        if(chars[i] == chars[j + 1]){
            j++;
        }
        next[i] = j;
    }
}
```

