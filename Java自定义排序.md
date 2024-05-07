## java自定义排序
```
Arrays.sort(intervals, new Comparator<int[]>() {
            @Override
            public int compare(int[] a, int[] b) {
                int temp=a[0] - b[0];
                return temp==0?a[1]-b[1]:temp;
            }
        });
```
