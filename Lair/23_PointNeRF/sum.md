## 교수님과의 주제 토론


1. 나의 contribution : Dataset이 있지만, Dataset에 없던 새로운 view에서도 잘 작동할수 있다. (Dataset이 있는것이 문제되는 이유? 굳이 왜 다른view를 생성해내냐? Dataset에 다있고, 이미 그걸로 학습하면 되는데 But, 나는 Dataset에 없는 새로운뷰도 multi view를 생성하고 Nerf를 할수 있다. -> slam은 항상 새로운 view를 본다)

2. 나의 또다른 contribution : 2D -> 3D는 instance level로 잘안된다. 하지만 multiview를 사용하면 instance 까지 잘된다 (어떤 의미? 의자사진주면, 의자스러운것 어떤의자인지는 모름 그냥 classification 했을때 의자인것같은애 만들어지는데, input 이미지랑 굉장히 비슷한 instance 성질을 유지하는 것을 만들수 있게 된다. (classfication : 그냥 의자다 아니다, instance : 의자 1번 의자 2번 구분가능))

3. contribution : image 사용하는 어떤 nerf모델이던 간에 사용하면 더 성능이 좋아진다. -> 어떤 모델이던지 적용가능하다.


=> 즉 나는 하나의 이미지가 들어오면, 다른 view에서의 image를 생성하여서 그거를 nerf 학습하는데 사용하여 더 좋은 f(x)를 만들어 낸다. 

-> 달성해야 하는 조건1 : 이미지 1개 널프 vs 이미지 1개 + muptiview생성한 널프 에서 후자가 좋아야함.
-> 조건 2 : multiview로 생성해낸 이미지 < nerf로 그시점의 cop에서 본 이미지가 화질이나 정확도가 더 좋아야함



- 내가 해야할것! multi view를 생성하는 알고리즘을 찾기! 아니면  panorama논문 (Shuran song 저자/ panoramic view sythesys)인것임

- 추가 idea 주신것, 실제 받은 input 한장은 진짜 real 이고, multiview로 생성해낸 이미지들은 부정확하다. 그렇기때문에 nerf를 학습할때 real image에 가중치를 더 두는 것! 

## summary

널프를 학습하는 법 : 카메라 pos + image이면, 어떤 공간을 생각한다. 그리고 cop에서 Ray를 이미지에 쏜다. discrete하게 쭉 곱하면서 물체가 차있는데까지 계산한다. (아 여기까지 들어가면 물체가 있구나, 여기 Pixel에서는 여기까지 들어가면 되구나를 안다.) 그렇게 공간상에 물체의 형체를 표현하는것이 점점 구체화 되면서, x,y,z를 넣었을때 어느정도 차있다 아니다를 표현하는 f(x,y,z) -> density, radiance 결과가 나오는 것이다. 그걸 input된 여러장에서 하는데 사진이 많을수록 효율 당연히 좋음. 


rendering 이란? : 렌더링은 마찬가지로, 보고싶은 pos에서 ray를 쏘아서 어디까지 가서 차있나? 를 학습한 f(x,y,z)로 확인하고 차있으면 그 pixel에 정보를 입력한다. 그럼 다른 cop에서 본 view를 얻을수 있고, 영상으로 rendering한다는것은 여러 view에서 f()를 통해 얻은 이미지를 영상으로 만드는 것이다. 



backbone -> 기본 골자, 뼈대를 의미 

예를 들면 VGG, RES 같이 가져와서 이걸 뼈대로 쓴다 하는 것과 같은것이다. 

ablation study -> 이것 저것 추가, 삭제하며 실험하는 것이다. 

예를 들면, 생성모델 수업에서 모듈을 추가했을때 뺐을때, 성능을 모두 측정하는데 모듈이 3개라면 8줄의 표로 성능을 정리할수 있다. 


경수친구의 아이디어 = point++ net은 네트워크 앞뒤가 한정되어서 좋은 네트워크가 나올시 사용할수 없다. 그렇기 때문에 확장성을 가진 어느 네트워크 backbone의 네트워크가 와도 그걸 이용가능한 것을 만들고 싶다. 그래서 새로운 구조를 제안하는데, 이런 경우 기존 보다 최소한 성능은 비슷하게 나와야 한다. 왜냐하면 contribution이 확장성이기 때문에, 더 좋으면 물론 좋겠지만 성능이 똑같아도 확장성 장점이 추가된것이기 때문