# Summary


1. 기본 AE와 달리 VAE에는 mu, logvar 이 있어서 kldivergence 이용하는것 같음
2. VAE와 GAN은 목적이 같다.
3. 단순 generation (input과 같게)가 목적이라면 kldivergence는 방해만 된다. 
4. 대부분 task를 opti = Adam, lr = 1e-4로 하면 학습 잘된다. 
5. VAE에서 latent로 사용하는것은 mu,var이 아니라 train 에서 return 값인 mu + e^val/2*eps 이다. (test에서는 그냥 mu 리턴값으로 사용)

# Coding tip

1. instance norm, Batch norm 쓸꺼면 model에서 통일해주는게 좋다.
2. activation fuc도 마찬가지이다. (다르게하면 forward, backward 전파속도 달라짐)
3. Encoder에서 마지막 layer도 activation fun 사용해라. 안쓰면 의미를 잃어버린다 -> feature 쓸꺼빼고, hidden layer는 모두 act fuc 사용.
4. 주로 conv conv 사이에 nomal, activate 쓰는데 이 두순서는 바뀌어도 성능차이 없는듯, con nomal act 순서가 일반적이긴 한듯
5. 안될때는 데이터셋 check, batch size, loss define, optimizer, network archi 등등을 고려해보자