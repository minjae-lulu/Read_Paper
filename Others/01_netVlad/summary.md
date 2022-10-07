## Summary

1. super glue 논문 : shift 등 피쳐뽑은것을 matching할때 nearlist search로 찾는데 이렇게 하지않고, GNN(graph neural net)을통해 한방에 matching시켜주는것

2. point Net 논문 : pointcloud는 들어올때 순서가 없다. 점하나 하나 들어왔을때, 하나가 더 들어오면 (ordering해도 N이 차이가나면 밀린다. 물체 표현하는 점의 갯수가 달라지면 밀린다는 의미) 이를 해결하기 위해, 한점에서 뽑은 피쳐가 128*1 벡터라고 하고 이런 점들이 여러개 있다고 생각할수 있음. 
이러한 여러 점이 들어와도 상관없게 하기위해, column기준으로 max값을 취해주고, 그것을 net에 넣어서 분류한다. 이렇게 하면 점이 더 늘어나도 128*1 크기를 일정하게 유지해서 net에 넣을수 있고, 값도 거의 변하지 않는다. 

3. PointVladnet 논문 : 이미지가 아니라 pointcloud도 input으로 해보자! p1, p2, 순서 없이 들아가는데 순서 달라져도 ㄱㅊ다는것을 수학으로 증명했음.
loss를 sum이 아닌, 특정값의 max로 정의해서 빠르게 하였음. 단점은 계속 같은구조 반복되거나 가려지면 성능이 안나옴

4. PatchnetVlad 논문 : view point 달라지면 성능안좋은것을 해결하기 위함. global + local로 하였음. global은 모든 image를 사용하여 vladvec(피쳐개념)을 뽑는것, local은 이미지 쪼개서 그것에서 vlad vec 뽑음. 2stage -> 1stage로 바꾼것이라 할수 있음. 먼저 global해서 net넣고 하는것 같음. 결과적으로 veiw point, 조도, 날씨 변해도 잘 수행함. 하지만 동적일때는 성능이 안좋아서 필요시 동적문체를 제거하거나 하는 방법을 써야함.